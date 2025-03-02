
pipでPDFMinerをインストールして日本語PDFからテキスト抽出をしたら以下のようになってしまった問題。
> 私(cid:888)、知的生産術(cid:887)良(cid:845)参考書(cid:853)欲(cid:864)(cid:845)(cid:880)(cid:866)。人(cid:884)知的生産術(cid:923)教(cid:849)(cid:916)
解決策: see [[PDFからのテキスト抽出]]

-----
調査過程のメモ
- [Still have issues with CID Characters · Issue #39 · euske/pdfminer](https://github.com/euske/pdfminer/issues/39)
    - 2014年
    - [[CMap]]を作り直す必要があるという指摘
- [pdfminer - PDF text extraction returns wrong characters due to ToUnicode map - Stack Overflow](https://stackoverflow.com/questions/28678841/pdf-text-extraction-returns-wrong-characters-due-to-tounicode-map)
    - 2015年
    - [[ToUnicode map]]に関しての話
- [python - What to do with CIDs in text extracted by PDFMiner? - Stack Overflow](https://stackoverflow.com/questions/50773909/what-to-do-with-cids-in-text-extracted-by-pdfminer)
    - ToUnicode mapに関しての話
- [How can I extract embedded fonts from a PDF as valid font files? - Stack Overflow](https://stackoverflow.com/questions/3488042/how-can-i-extract-embedded-fonts-from-a-pdf-as-valid-font-files)
    - 埋め込まれたフォントを抜き出せるか？という議論
- [PDFMinerでPDFから日本語テキストを抽出する](https://qiita.com/korkewriya/items/72de38fc506ab37b4f2d)
    - 二点しんにょうなどがCIDに置き換えられたという報告
- [Pythonで「PDFからテキストデータを抜いて使う」のを試してみました（pdfminer.six) - アラカン"BOKU"のITな日常](http://arakan-pgm-ai.hatenablog.com/entry/2018/01/07/080000)
    - 2018
    - コマンドラインでは無くスクリプト内からインポートして使う例
    - こちらも僕の環境と同様にひらがながCIDになっている