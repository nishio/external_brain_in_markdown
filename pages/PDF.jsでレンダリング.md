
[PDF を Gyazo に展開して Scrapbox の記事にして全文検索する - Diary](https://diary.app.ssig33.com/474?fbclid=IwAR3TbTubD3eiU_TjTUMsmiwI-1iImJwejshTs4Ob4qRdwNNojd4Z-qVMBd8)
> PDFをドラッグ&ドロップ
> [[PDF.js]] でレンダリング
> 全てのページを Gyazo にアップロード
> Scrapbox のページを作成

自分の手元でも似たようなことを実現してた
- [[PDFからPNGへの変換]]を使う
- Automatorからcurlを叩く仕組みを使ってる人もいる
だけど、他の人に提供するのにはサーバを作るのがコスト面で面倒だなーと思って放置してた
この手法はJSでPDFのレンダリングを行うことで、ブラウザ拡張の形にパッケージ化できている

検索は「[[Gyazo上での検索結果をScrapbox上で表示]]」というアプローチ
- 「[[GyazoのOCRテキストをScrapboxに置く]]」ではない
