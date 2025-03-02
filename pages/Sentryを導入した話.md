---
title: "Sentryを導入した話"
---

[[Sentry]]を導入した話
- 今回はクライアントサイドに入れたけども、サーバサイドにも入れた方がいいなと思った
- サーバサイドでもクライアントサイドでも対話IDを追加で送るべきだなと気づいた

[https://keicho.netlify.app/#talk=liJIAQmmJQIuUkKijd6d](https://keicho.netlify.app/#talk=liJIAQmmJQIuUkKijd6d)

<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>あなたはこの会話で何が起きて欲しいですか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>Sentryを導入した話をしたい
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>その「Sentry」は、どんな「Sentry」ですか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>ユーザの手元のブラウザ上でエラーが起きた時にそれを開発者に伝える機能です
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>その「ユーザ」は、どんな「ユーザ」ですか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>ユーザが僕でかつPCで操作してる時にはエラーログが何もしなくても見れるのだけど、それ以外の時には見れないからこういう仕組みが必要だった
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>その「ユーザ」について、他に何かありますか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>エラーが起きた時に内容をつたえてくれるわけじゃないから、システム自体に伝える機能を入れておくわけ
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>その「エラー」は、どんな「エラー」ですか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>例えば最近、直前の会話を再開する機能をつけたんだけど、そうすると自分の開発マシンではエラーにならないけど「直前の会話」の存在しないユーザの手元でだけエラーになるって問題が発生していて、そういうのに気づくのはシステムに手助けしてほしいなぁと思うわけです
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>その「エラー」について、他に何かありますか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>どういう操作をしてそのエラーが起きたかも記録されるのでデバッグが捗る
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>その「エラー」は、どこにありますか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>ユーザの手元にある
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>あなたはその「ユーザ」をどう知るのですか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>ユーザが具体的に誰であるかは知らないのだけど、ブラウザとかOSとかの情報はわかる
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>その「ユーザ」は、どこにありますか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>僕と離れたところにいるから僕が直接観察できないわけ
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>あなたが価値を感じているのは何ですか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>離れたところにいるユーザの手元で起きたエラーの情報を詳しく速やかに通知してくれることで、問題を見つけやすくなるし、解決もしやすくなる、というところだな
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>あなたはその「エラー」をどう知るのですか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>メール通知される
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>
- >  離れたところにいるユーザの手元で起きたエラーの情報を詳しく速やかに通知してくれることで、問題を見つけやすくなるし、解決もしやすくなる、というところだな
- この「エラー」は、どのあたりにありますか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>ユーザの手元のブラウザ上、あ、そうだ、サーバ上のエラーも同じように通知させられるので、それもやった方がいいね。早く気づく、という価値のためには。
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>その「エラー」に関して、何が起こるとよいですか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>速やかに解決されると良い
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>それには「エラー」に何が起こる必要がありますか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>解決のために必要な情報とセットで通知されると良い
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>「エラー」に関して、それができますか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>必要な情報として何があれば十分なのかは未知だな。サーバ上の方は対話IDを送信した方が良さそう。
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>
- >  ユーザの手元のブラウザ上、あ、そうだ、サーバ上のエラーも同じように通知させられるので、それもやった方がいいね。早く気づく、という価値のためには。
- この「ユーザ」は、どこから来るのですか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>具体的なユーザを取得してないから、クライアント版でも対話IDを送信した方がよさそうだな
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>その「ユーザ」は、どのあたりにありますか？
