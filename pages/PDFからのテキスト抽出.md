
2023-09-12
- テキストと画像を対応づけてクラウドに置くことまで含めて[[Gyazo Pro]]に任せる

2023-04-07
- [[PDFからPNGへの変換]]してから[[Google Cloud Vision]] APIを使う(予定)
    - 無償のツールでノイジーなデータを作って後で頑張るより課金したほうが良いという判断

2022-03-29 3行まとめ:
- `$ pip3 install pdf2txt.py`
- `$ pdf2txt.py -V -o <outfile> <infile>`
- 新しいスクリプトを作ろうと考えてるので詳しいことはできてから加筆する

2020-09-28 3行まとめ:
- `$ pip install pdfminer.six`
- `$ pdf2txt.py -V -o <outfile> <infile>`
- [https://github.com/nishio/ja_pdf_to_text](https://github.com/nishio/ja_pdf_to_text)
    - [[ja_pdf_to_text]], [[PDFMiner]]

2018-09-24 1行まとめ: PDFMiner.sixのリポジトリをcloneしてCMapを生成してからsetup.py install

以前[[word2vecによる自然言語処理]]を書いた時には[PDFMiner](https://www.unixuser.org/~euske/python/pdfminer/)を使った。
単なるテキスト抽出には当時のスクリプトを使い回していたがいろいろ新しいことをやりたくなった。
2018年現在、PDFMinerはPython2のみサポートなので、2/3対応の[PDFMiner.six](https://github.com/pdfminer/pdfminer.six)を使う。

まとめ
- Python3で使いたいのでPDFMiner.sixを使う
- 日本語PDFを扱う上ではCMapの生成が必要
    - pipでインストールするとどうやって生成するかわからないのでリポジトリからcloneする
    - `make cmap`せよと書いてあるが`make: Nothing to be done for cmap.`と言われる
    - Makefileに書かれているコマンドを明示的に叩いた(下記) #CMapの再生成
        - make cmap_cleanでもよかったかもしれないが試してない
- `$ python setup.py install`
    - 先にpipで入れてた場合はuninstallしとくこと
- `$ pdf2txt.py -V -o <outfile> <infile>`
これで綺麗なテキストファイルが得られるようになった

備考
- [[poppler]]に同梱されている[[pdftotext]]だと、一見すんなり変換できたように見えるが、行の順番に直感的ではない乱れが発生する。(おそらく脚注やページ端の章見出しなどのイレギュラーなバウンディングボックスで混乱している)

CMap生成コマンド
sh

```
python tools/conv_cmap.py -c B5=cp950 -c UniCNS-UTF8=utf-8 pdfminer/cmap Adobe-CNS1 cmaprsrc/cid2code_Adobe_CNS1.txt
python tools/conv_cmap.py -c GBK-EUC=cp936 -c UniGB-UTF8=utf-8 pdfminer/cmap Adobe-GB1 cmaprsrc/cid2code_Adobe_GB1.txt
python tools/conv_cmap.py -c RKSJ=cp932 -c EUC=euc-jp -c UniJIS-UTF8=utf-8 pdfminer/cmap Adobe-Japan1 cmaprsrc/cid2code_Adobe_Japan1.txt
python tools/conv_cmap.py -c KSC-EUC=euc-kr -c KSC-Johab=johab -c KSCms-UHC=cp949 -c UniKS-UTF8=utf-8 pdfminer/cmap Adobe-Korea1 cmaprsrc/cid2code_Adobe_Korea1.txt
```



抽出例
![image](https://gyazo.com/ace0fa36a067600a48c2ea4e4b9391db/thumb/1000)
cmap生成後のPDFMinerでの結果
> この本の目的
>
>  　私は、知的生産術の良い参考書が欲しいです。人に知的生産術を教える
>  ときに、お勧めできる本が欲しいです。
>  　私は、サイボウズで知的生産性の研究に10年間従事してきました注1。業
>  務の一環として、京都大学サマーデザインスクールで、考えを整理してア
>  ウトプットする方法のワークショップを行ったり、首都大学東京の非常勤
>  講師として、大学生に研究によって新たな知識を生み出すことについて教

-----以下失敗ログ

pipで入れたPDFMinerでの結果
> この本の目的
>
>  　私(cid:888)、知的生産術(cid:887)良(cid:845)参考書(cid:853)欲(cid:864)(cid:845)(cid:880)(cid:866)。人(cid:884)知的生産術(cid:923)教(cid:849)(cid:916)
>  (cid:881)(cid:854)(cid:884)、(cid:851)勧(cid:906)(cid:880)(cid:854)(cid:916)本(cid:853)欲(cid:864)(cid:845)(cid:880)(cid:866)。
>  　私(cid:888)、(cid:945)(cid:928)(cid:984)(cid:930)(cid:950)(cid:880)知的生産性(cid:887)研究(cid:884)10年間従事(cid:864)(cid:879)(cid:854)(cid:903)(cid:864)(cid:872)(cid:2987)1。業
>  務(cid:887)一環(cid:881)(cid:864)(cid:879)、京都大学(cid:945)(cid:986)(cid:660)(cid:963)(cid:946)(cid:928)(cid:1007)(cid:949)(cid:939)(cid:660)(cid:999)(cid:880)、考(cid:849)(cid:923)整理(cid:864)(cid:879)(cid:926)
うーん、CIDフォントの埋め込みになっているぞ。[[CID問題]]

[[poppler]]に同梱されている[[pdftotext]]だとこうなる
> この本の目的
>  私は、知的生産術の良い参考書が欲しいです。人に知的生産術を教える
>
>  ときに、お勧めできる本が欲しいです。
>  私は、サイボウズで知的生産性の研究に 10 年間従事してきました注 1。業
>  務の一環として、京都大学サマーデザインスクールで、考えを整理してア
>
>  ウトプットする方法のワークショップを行ったり、首都大学東京の非常勤
>  講師として、大学生に研究によって新たな知識を生み出すことについて教
>
>  えたりしてきました。しかし、限られた時間では伝えたいことが伝えきれ
>  えません。私の伝えたいことが 1 冊にまとまった本が欲しいです。
>  でも、ちょうど良い本がないんです。何か 1 冊だけお勧めするなら川喜
>  『発想法』注 2 ですが、これは 1966 年の本です。抽象的な考え方は今
>  田二郎の
>
>  この本の目的
>
>  ません。参考書を紹介しても、たくさん紹介したのでは全部は読んでもら
一見良いように見えるかもしれないが、最終行の「ません。参考書を紹介しても〜」はその8行上の「限られた時間では伝えたいことが伝えきれ」の続き。「川喜」「田二郎の」「『発想法』注 2」という並びもおかしくなっている。

PDFMinerでは同じ範囲が適切に並べられている。
>  えたりしてきました。しかし、限られた時間では伝えたいことが伝えきれ
>  ません。参考書を紹介しても、たくさん紹介したのでは全部は読んでもら
>  えません。私の伝えたいことが1冊にまとまった本が欲しいです。
>  　でも、ちょうど良い本がないんです。何か1冊だけお勧めするなら川喜
>  田二郎の『発想法』注2ですが、これは1966年の本です。抽象的な考え方は今
>  でも十分有効ですが、具体的な方法論が50年前の技術水準を前提にしてい

[[PDFMinerの座標系解析]]