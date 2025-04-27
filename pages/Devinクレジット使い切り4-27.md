---
title: "Devinクレジット使い切り4/27"
---

from [[日記2025-04-27]]
Devinクレジット使い切り
216.68 ACUs
残りクレジットを消費するアイデアを思いついたぞ
> [https://github.com/nishio/external_brain_in_markdown](https://github.com/nishio/external_brain_in_markdown) これは作者の外部脳です
>  これを読んで「実装すべきだと思ったけどまだ着手できてないアイデア」を見つけて番号付きリスト形式で示してください
イマイチだったw
- 論文のメモのfuture workを拾ってしまった

いやー、進めたいプロジェクト自体はたくさんあるんだけどね
- Kozanebaとか
- AIPMとか
簡単に実行できるタスクの形に落ちてないんだよな
- そしてタスクにするところは高度な意思決定を伴うのでDevinに丸投げできるわけではない

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>Devinのトークンが40余ってて期限は今日です、どうしたらいい？
<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>
- ✅ コード全体の静的解析＆リファクタ提案
- ✅ README・関数コメントの自動生成／更新
- ✅ テストケース自動生成（例：TestGen-LLM 風）
- 「あとで読む」用アウトプットを作る
    - 例：技術スタック全体のアーキ図、依存関係グラフ、脆弱性レポート、改善ロードマップ…
    - 生成物は Markdown／HTML／PDF で保存しておけば、トークン失効後も活用できます。

Kozaneba
- [https://app.devin.ai/sessions/f20984a03b224d228b288e0e4244129f](https://app.devin.ai/sessions/f20984a03b224d228b288e0e4244129f)
- [https://app.devin.ai/sessions/40113237620548d9b7af6359dc360cb2](https://app.devin.ai/sessions/40113237620548d9b7af6359dc360cb2)
- iPadで動かない問題の修正
    - [https://app.devin.ai/sessions/1a484adb43ae45c1ac2da066c4171528](https://app.devin.ai/sessions/1a484adb43ae45c1ac2da066c4171528)
- [https://app.devin.ai/sessions/84544e87ab7c4dc2bcfdf7712bcfd2ec](https://app.devin.ai/sessions/84544e87ab7c4dc2bcfdf7712bcfd2ec)
- あっ、Kozanebaのバグレポートが2件きていた
    - 気づいてなかった
    - 雑にDevinに投げておこう
    - なんと両方「直った」と言ってる
AIPM
- [https://app.devin.ai/sessions/bc016a2e8e8e4c65968c898993152e49](https://app.devin.ai/sessions/bc016a2e8e8e4c65968c898993152e49)
keichoのコードどこだっけ
- netlifyをみてgithubをみてフロントエンドだけじゃんとなった
- vercelにもない
- herokuだった
- > The Heroku-20 stack is deprecated
- >  This app is using the Heroku-20 stack, which is deprecated. From April 30th, 2025, Heroku-20 will be end-of-life and no longer receive security updates. From May 1st, 2025, builds will be disabled. Please upgrade your app to a newer Heroku stack.
- うわあ、heroku自体のgitにpushしてたのでローカルとherokuにしかコードがないぞ、そういうことか
    - GitHubにprivate repoを作ってpushしておこう
- 時代を感じさせるな
    - 当時GitHubのprivate repoは数が限られており、無制限だったbitbucketをメインで使っていた、たぶん
    - WebUIができる前のCUI版keicho botはbitbucketにある
        - bitbucketどうやってログインするんだっけ、まあいいか()
[http://www.teratti.jp/heart/hew/download/index.htm#h_develop](http://www.teratti.jp/heart/hew/download/index.htm#h_develop)
- 古いソフト繋がりで思い出した
    - よくサイトを維持してくれたものだ、何年経っただろう
    - 25年前に作られたDelphiのコード
    - ソースコードがZIPですらない、LZHだw

Kozanebaの発展がすごい
- ユーザのバグ報告をそのまま投げつけるだけで直ったっぽい
- コードを読ませて改善点を報告させてissueにさせる
- issueの中から良さそうなものを選んで実行させる
    - 大きすぎるissueなら分解してと言う
- CIが通ったやつは気にせずマージ

Keichobotをリファクタしたいと言う
- テストでカバーしてねと言う
    - mecabがこけてると言う
    - o3に聞いてつたえる
    - > Python 3.12との互換性のために、mecab-python3のバージョンを0.996.5から>=1.0.9に更新しました。


<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>Netlifyのデプロイチェックが失敗している原因は？
<img src='https://scrapbox.io/api/pages/nishio/devin/icon' alt='devin.icon' height="19.5"/>Netlifyのデプロイ失敗の原因は、reactnパッケージと@types/reactのバージョン競合です。reactnは@types/react@^16.8.0を要求していますが、プロジェクトは@types/react@17.0.52を使用しています。この問題を解決するために.npmrcとnetlify.tomlファイルを追加しましたが、Netlifyの設定に関する追加のアクセス権が必要かもしれません。
<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>ざっくりまとめると、Netlify 側の npm v7 以降が “peerDependencies 衝突” をエラー扱い するため、
reactn が要求する @types/react@^16.8.0 と、あなたのプロジェクトが入れている @types/react@17.x がかち合ってインストールが止まっています。ローカルで通るのは npm v6 以前を使っていて警告止まりだから、という典型パターンです。 ...
<img src='https://scrapbox.io/api/pages/nishio/devin/icon' alt='devin.icon' height="19.5"/>提案された方法のうち、最もクリーンな「A. 依存を揃える」アプローチを試してみます。reactnを最新版2.2.6にアップデートし、package-lock.jsonを再生成してから再デプロイします。進捗状況は随時お知らせします。


寝て起きた
- 無事期限切れするACUを使い切ることができた！
- そしてそのあとすぐ従量課金モードに切り替わった
