
クックパッドが社内データで[[BERT]]を自前学習した経験談
[BERT with SentencePiece で日本語専用の pre-trained モデルを学習し、それを基にタスクを解く - クックパッド開発者ブログ](https://techlife.cookpad.com/entry/2018/12/04/093000)

- > BERT の multilingual モデルは日本語の扱いには適さないので [[SentencePiece]] を使う
    - 関連 [[Google Bertのtokenizerで濁音が取れる理由]]
- >  pre-training にはクックパッドの調理手順のテキスト（約1600万文）を使用
- >  学習は p3.2xlarge インスタンスで 3.5 日程度学習
    - p3.2xlargeは3USD/hourなので2.5万ぐらい
