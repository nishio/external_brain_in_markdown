
関連: [[PDFからのテキスト抽出]]

2023-04-07
- 前にまとめてから5年も経ってるのでGPT4にオススメを聞いてみた
- 裁断スキャンPDFに対するGPT4の答え: [[PyPDF2]]
    - これはPDFによっては`KeyError: '/XObject'`になる
    - 下記2017年のまとめのように画像埋め込みがされてないとエラーになるのだろう
- 一般のPDFについてのGPT4の答え: [[pdf2image]]
    - `$ pip install pdf2image`
    - これは内部的には[[pdftocairo]]を使う、pdftocairoは[[poppler]]のツール
    - `$ brew install poppler`
python

```
    from pdf2image import convert_from_path
    images = convert_from_path(pdf_path)
    for i, image in enumerate(tqdm(images)):
        image.save(os.path.join(output_dir, f"{i+1}.png"), "PNG")
```

    - 出力の例
        - ![image](https://gyazo.com/e475b087b9ff628e9d78baa62758e604/thumb/1000)
        - デフォルトだと72dpi

2017-08-23
- まとめ
    - gsは画質が酷い、ImageMagick(convert)も内部でgsを使う。pdftoppmはマシだが、[[pdftocairo]]が一番良い。
        - `pdftocairo -r 200 -f 0 -png mybook.pdf prefix`
    - 裁断スキャンPDFに関してはpdfimagesで埋め込まれている-r 300相当の画像を取り出すのが最も綺麗
        - そういうPDFかどうかの判断が必要なのが問題。
    - pdftocairoはpdfimagesとほぼ変わりない品質。ただし48倍遅い

- gs
    - `$ time gs -q -dBATCH -dNOPAUSE -sDEVICE=png16m -r100 -sOutputFile=pages_%04d.png mybook.pdf`
    - `gs -q -dBATCH -dNOPAUSE -sDEVICE=png16m -r100 -sOutputFile=pages_%04d.png   219.36s user 5.22s system 95% cpu 3:54.68 total`
    - 552x823
    - ![image](https://gyazo.com/c9f7451a31da4c565fd3ef0b10f784bf/thumb/1000)![image](https://gyazo.com/307ffe755412681e1de74d138b4b2832/thumb/1000)
    - 酷いジャギジャギ

- pdftoppm
    - `$ time pdftoppm -r 100 -png mybook.pdf mybook`
    - `pdftoppm -r 100 -png mybook.pdf mybook  464.95s user 6.77s system 96% cpu 8:07.62 total`
    - 552x823
    - ![image](https://gyazo.com/cfda2fb38aebcfdc7cbc6d6de3b34303/thumb/1000)![image](https://gyazo.com/6e07e92a8638865780d6aa54dc2cb3cf/thumb/1000)
    - だいぶマシ

- pdftoppm 2倍の解像度で出力
    - `$ time pdftoppm -r 200 -png mybook.pdf mybook`
    - `pdftoppm -r 200 -png mybook.pdf mybook  1104.28s user 12.22s system 96% cpu 19:14.59 total`
    - 1104x1646
    - ![image](https://gyazo.com/790a870887bba282ad6bb12d1d869bff/thumb/1000)![image](https://gyazo.com/4e31fcad5aba227fc490bf350a00f962/thumb/1000)
    - 題字の雰囲気がだいぶ変わった？(細くなった？シャープになった印象)
    - 2倍のサイズで出した後上記サムネイルでは2倍に縮小される。その過程で文字が細くなる？

- ではgsで2倍の解像度で出したらどうなるか
    - `$ time gs -q -dBATCH -dNOPAUSE -sDEVICE=png16m -r200 -sOutputFile=pages_%04d.png mybook.pdf`
    - `gs -q -dBATCH -dNOPAUSE -sDEVICE=png16m -r200 -sOutputFile=pages_%04d.png   619.65s user 13.83s system 93% cpu 11:14.36 total`
    - ![image](https://gyazo.com/9ce844ae4f2c48c58dcc300e916b0f1f/thumb/1000)![image](https://gyazo.com/39f68f800e536c4b268bda4213c5396c/thumb/1000)
    - 汚い
    - 明朝体の「変」の横画などが消えている
    - 拡大(左:gs、右: pdftoppm)
    - ![image](https://gyazo.com/7d3d0371af344c56ee8ce7ddfa66f05d/thumb/1000)
    - gsは1ピクセル1回しかサンプリングしてなさげ。pdftoppmは何回かサンプリングして混ぜ合わせている挙動にみえる。

- ImageMagick(convert)
    - `$ time convert -verbose -density 200 mybook.pdf pages_%04d.png`
    - `"gs" -q -dQUIET -dSAFER -dBATCH -dNOPAUSE -dNOPROMPT -dMaxBitmap=500000000 -dAlignToPixels=0 -dGridFitTT=2 "-sDEVICE=pngalpha" -dTextAlphaBits=4 -dGraphicsAlphaBits=4 "-r200x200"  "-sOutputFile=/tmp/magick-le3ab9PT-%08d" "-f/tmp/magick-s7CciX7v" "-f/tmp/magick-6huEpaq8"`
    - ![image](https://gyazo.com/9a73370c5cbcc45a1b740dc3e7f9267a/thumb/1000)![image](https://gyazo.com/c36f8d7fb55966b464c6397be100b506/thumb/1000)
    - コマンドラインの出力からわかるように、内部的にはgsを叩いている。画質もgs同様。

- pdfimages
    - `$ time pdfimages -j mybook.pdf ./pages`
    - `pdfimages -j mybook.pdf ./pages  6.14s user 2.51s system 59% cpu 14.569 total`
    - 対象PDFの中の画像ファイルを取り出す
    - 実験対象PDFが紙の書籍の裁断スキャンであるので、スキャン結果が画像ファイルで入っている
    - ![image](https://gyazo.com/112c27b96232c0d73b64c0c702265959/thumb/1000)
    - 1656x2469
    - gsやpdftoppmの-rオプションが100の時552x823だったので、-r 300 相当。
    - 同一解像度に縮小してみる
        - `$ convert -thumbnail 1104x1646 ex7/pages-002.jpg t.png`
        - `convert -thumbnail 1104x1646 ex7/pages-002.jpg t.png  3.86s user 0.09s system 98% cpu 4.002 total`
    - ![image](https://gyazo.com/ea73b2a3aefcc02a69a3ce949db11784/thumb/1000)![image](https://gyazo.com/317d4bf8891c5e1e60aa244cc5790c52/thumb/1000)
    - きれいではあるが、PDFの出自を選ぶ

- pdftocairo
    - `$ time pdftocairo -r 200 -f 0 -l 10 -png mybook.pdf pages`
    - `pdftocairo -r 200 -f 0 -l 10 -png mybook.pdf pages  27.02s user 0.29s system 79% cpu 34.260 total`
    - ![image](https://gyazo.com/63792a9552169c1a0f71b15c69b10759/thumb/1000)![image](https://gyazo.com/8ec5f57781eea1a4e16f3ae8f118e26c/thumb/1000)
    - 拡大(左上gs、右上pdftoppm、左下pdfimagesして縮小、右下pdftocairo)
        - ![image](https://gyazo.com/3c493d7126c0692c284717ff2c536c19/thumb/1000)
        - pdfimagesから縮小したものとほぼ同等の出力
        - イコールではないが、1ライン切りだして、並べてじっくり見たら差がわかる、ぐらいの僅差
    - 10ページで34秒掛かっており、割と遅い(pdftoppmで270ページ出すのに19秒なので、ざっくり48倍遅い)

2017-08-23