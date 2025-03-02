
from [[日記2023-06-13]]
prev [[pVectorSearch2023-06-07]]

[[非公開資料をベクトル検索対象にする]]
- 事故る予感しかしない
- まず公開Scrapboxから作ったデータに関してpublicフラグをつける
    - そしてデフォルトの検索をpublicからの検索にする
    - これデータ入れ直すならupdate機能を追加してない現状でも先に再クロールしたらいいんでは？
- privateは多様なのでprivateフラグではなく個別のタグにする
- 特定の権限を持つ人だけ検索対象一覧に特定のタグを持つレコードを検索対象に加えるチェックボックスを表示する

特定の人だけ検索対象を追加する
- 特定の人に権限を与える作業、僕が作業するのはミスりそうなので、インバイトコードにしたい
- そもそもこの機能の実装でバグりそう

NotionはMarkdownでサブページごとエクスポートできそう
- ![image](https://gyazo.com/b7524c5f56157b4ba95ae507441b5577/thumb/1000)


> これデータ入れ直すならupdate機能を追加してない現状でも先に再クロールしたらいいんでは？
- ✅全部まとめて再クロール、5分くらい
JSONからのembeddingはまだバッチにしてなかった
- ✅コードを一本化
embeddingまちの間に検索にフィルタをつける実験
- APIの呼び出し方はわかった
- UIからフィルターに関するデータを受け取らないといけない

Notionを検索対象にする話
- ヒットしたものをクリックしたら対象にジャンプして欲しいよね
- だけどScrapboxと違って「プロジェクトとページ名でリンク先が決まる」というわけではない
- UIのためのデータを考えないといけない
- 今回はある特定の非公開ページをサプページを含めてエクスポートしたもの
- ルートのページのURLがあったら復元できるのかな？
    - お、なるほど
        - ローカルファイル名
            - `提案2：西尾 7d7c95ceaeb446418bffe462034292bd.md`
        - このIDの部分が全世界ユニークIDのようだ
            - `notion.so/7d7c95ceaeb446418bffe462034292bd`で目的ページに飛べる
    - じゃあ `{type: notion, id: xxx}`かな〜

:

```
processing 15469 pages
100%|...| 15469/15469 [00:53<00:00, 290.87it/s]
processing 13893 tasks in 277 batches)
100%|...| 278/278 [11:27<00:00,  2.47s/it]
```


ん、これ僕の理解が正しければすんなり差分更新にできる実装になってるな
- 過去の自分、偉い

:

```
# halsk
processing 1281 pages
100%|...| 1281/1281 [00:02<00:00, 619.70it/s]
total tasks: 2221,  1.00% was cached
processing 0 tasks in 0 batches)
0it [00:00, ?it/s]

# yuiseki
processing 2778 pages
100%|...| 2778/2778 [00:09<00:00, 289.72it/s]
total tasks: 4738,  0.92% was cached
processing 375 tasks in 8 batches)
100%|...| 8/8 [00:25<00:00,  3.13s/it]

# tkgshn
processing 5750 pages
100%|...| 5750/5750 [00:11<00:00, 486.96it/s]
total tasks: 12117,  0.97% was cached
processing 308 tasks in 7 batches)
100%|...| 7/7 [00:20<00:00,  2.89s/it]
```


差分更新できた

Notionのエクスポートデータから各ページごとにタイトルとIDを取るコードはできた

残りは明日
TODO
- Notionからデータを作る
- Notionの検索結果のビューを作る
- 特定の権限の人だけUIを出す
- 特定の権限を確認して検索フィルターする
- UIからフィルターに関するデータを受け取る
- データをQdrantに入れ直す

2023-06-14
- Discordでの議論も検索対象に入れた方がいいなと思ったのでとりあえず今回は過去ログを日付で分割してNotionに貼ることにした
    - 各種論文のアブストをDeepLしてNotionに入れた
    - Google Docsにあった初期の議事録もNotionにコピペ

✅Notionからデータを作る
- Localのqdrantに入れて試す
    - ✅そのままだとヒットすることを確認
    - ✅publicだけからの検索ならヒットしないことを確認
✅Notionの検索結果のビューを作る
- 検索結果をクリックしてScrapboxとNotionとどちらにも飛べるようになった

特定の権限の人だけUIを出す
- うーん、めんどくさいな
- たとえば特定のキーがlocalStorageに入っていることを表示条件にしたらJSをリバースエンジニアリングしたらできてしまう
- 面倒でもログイン状態を確認すべきか
- GPT4と相談: [[Firebase Auth]]の[[Custom Claims]]で[[Feature Toggle]]する
    - [https://chat.openai.com/share/d4be9a75-1e8a-4a3a-b3fe-effaa1efc200](https://chat.openai.com/share/d4be9a75-1e8a-4a3a-b3fe-effaa1efc200)
    - あー、なるほどね、grantするAPIを作ってサーバサイドでやればいいのか
    - [サーバーに Firebase Admin SDK を追加する](https://firebase.google.com/docs/admin/setup?hl=ja)
    - GPT4の情報がちょっと古くて改行のエスケープはもう不要だった
        - こういうスキルはまだ必要
    - 表示はできた
- ![image](https://gyazo.com/d5a812c16b793709c754b33de850cff4/thumb/1000)![image](https://gyazo.com/3b8e53257a7bd9bd965c970a213faaee/thumb/1000)
    - できた

特定の権限を確認して検索フィルターする
- featureAがONの時に、その情報を検索APIにも渡す。そして権限があることを確認してからフィルターの設定に反映して検索する。
- いやこれ、チェックボックスで検索対象を切り替えられるようにすることと、特別な権限がある人だけ特別のターゲットを検索できるようにすることは別のイシューだな
- 一度にやると複雑だから後者だけ先にやろう
- できた

後は特定のユーザにCustom Claimつけるのを僕がDBをいじったりしないでできるようにする方法か
- promptでpasswordを取ってsetCustomClaim APIに送る
- なぜか前回は設定できたのに今回はできない？
- > Admin SDK でユーザーの新しいクレームが変更されると、次のように ID トークンによってクライアント側の認証済みユーザーに伝播されます。
- >  カスタム クレームの変更後に、ユーザーがログインまたは再認証する。その結果として発行された ID トークンには最新のクレームが含まれる。
- >  古いトークンが期限切れになると、既存のユーザー セッションでその ID トークンが更新される。
- >  currentUser.getIdToken(true) を呼び出して ID トークンが強制的に更新される。
    - [カスタム クレームとセキュリティ ルールによるアクセスの制御 | Firebase Authentication](https://firebase.google.com/docs/auth/admin/custom-claims?hl=ja)
- あー、なるほど、キャッシュされてるのか
- UIはさておき、できた
- カスタムクレームは追加されるべきだけど、今は上書きになっている、今は一つしかないから良いが二つ目をやる時に直す必要がある

![image](https://gyazo.com/1af1f02dd048cee348904a7d6e21973a/thumb/1000)
- ![image](https://gyazo.com/2497a73d671c1780bfe6ea10fb0e97b9/thumb/1000)

クラウド側にデータを送る
- 今回全部入れ替え
- インデクシングを止めるコードを入れても、バッチインサートごとに1秒待つようにしても`The write operation timed out`が出てしまう
- 失敗した時に10秒待ってリトライするコードに変えてみた
- ![image](https://gyazo.com/799c5be1d5ab2697891a269a0051f714/thumb/1000)
    - ほー、冒頭部で3回こけてるけど後は安定しているな
    - だとすると毎回sleepする代わりに、こけたときだけ大きめにsleepする今の設計が正しそうだな

iPhoneでひどくなる問題、PCでの再現方法わかった
- ![image](https://gyazo.com/73df1b8399016a56ed7d0a35b4b1257c/thumb/1000)![image](https://gyazo.com/478aafb16a5535e199fa1f307b4d43d8/thumb/1000)
- 直した

Vercel環境にデプロイするとこける
- 環境変数の設定し忘れ
    - .env.localを変えた時点でVercel側もやっとけばいいのでは？
- Firebaseの初期化を通らないパスがあった
    - ケアレスミス

動いた、めでたしめでたし
