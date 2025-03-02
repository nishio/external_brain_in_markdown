---
title: "AI時代のWebサービス"
---

AI時代の[[Webサービス]]
> [fladdict](https://x.com/fladdict/status/1882764245831721057) みんな[[GPT operator]]の真のポイントと脅威を理解してない。
>  AIがブラウザで各種代行をする時代、AIブロックしてるサイトは、買い物や調べ物やそもそも利用されなくなる… 可能性を突きつけられてるんやで。
- [[AIエージェント飲み会]]で経験した

> [hybridhybrid2](https://x.com/hybridhybrid2/status/1882834668342685872) アクセス解析というウェブマーケティングの基本の基本が使い物にならなくなる時代が、、、


> [kazunori_279](https://x.com/kazunori_279/status/1882850028911493617) というかブラウザやHTMLもはやいらなくね？　LLM用の認証とRPCとsemanticなservice discovery基盤があればいいのだ。
> [kazunori_279](https://x.com/kazunori_279/status/1882856575821574321) 最終的にAIエージェントが人に見せる時だけHTMLやUIが必要になるけど、その裏側でエージェントが数十や数百のサイトで検索したり決済する部分はHTMLもUIもいらない。public MPCみたいな基盤だけ残ると思う。
> [kazunori_279](https://x.com/kazunori_279/status/1882857142685942201) Expediaみたいな感じかな。全てあれになるのかも。


> [nishio](https://x.com/nishio/status/1883091683493249315) モバイル向けにサービス開発してからデスクトップ向けの画面を作ってたのと同じように、AI向けにサービスを作ってからそれの人間向けの画面を作るって開発スタイルが生まれて、開発体力がないところは人間向け画面が雑になる(AI向けの方がテストしやすいし)
- [[モバイルファースト]]から[[AIファースト]]へ


> [takiuchi](https://x.com/takiuchi/status/1883195490856223098) AI向けサービスの問題は、AIのデータ処理能力が高すぎるから一度出したデータは丸ごと持っていかれるようなものなので従量課金が成立しないって事だよな。会社ごと買ってもらうならありだけど

---

> [kenn](https://x.com/kenn/status/1883468583096688977) 「モバイルファースト」の次には「オペレーター（エージェント）ファースト」が来るぞ、という話。JSコード減らしてAriaで宣言的に要素の役割を書けばアクセシビリティ的にも一石二鳥。
>  なんならエージェント専用のJS関数をコールできるようにするところまで行くかもね。
>  >[threepointone](https://x.com/threepointone/status/1883468583096688977) “operators” should/will eval javascript
>  we’re already talking about building websites and apps that will be easier for LLM driven automation / “operators” to, er, operate. it’ll start with simplified dom and css, clearer aria descriptions, a resurgence of non-js driven forms,
>  "operators" は JavaScript を評価するべきです/するでしょう
>  私たちはすでに、LLMドリブンオートメーション/「オペレーター」が操作しやすくなるWebサイトやアプリの構築について話しています。それは、簡素化されたDOMとCSS、より明確なAriaの説明、非JS駆動のフォームの復活から始まります。

> [nishio](https://x.com/nishio/status/1883498681460244582) そしてオペレーターを介するコンピュータウイルスが登場して企業からの漏洩事件が起き、禁止する企業が出てくるところまでほぼ確定済みの未来だと思う
> [ringo](https://x.com/ringo/status/1883508015250497705) マイクロソフト365についてるオペレーターだけはOKという企業が出てくる未来もだいたい見えてるかも。。
> [nishio](https://x.com/nishio/status/1883510018831708358) あるあるすぎる！

> [nishio](https://x.com/nishio/status/1883528722416112033) まあでもこれ、操作だけログに残る人間と、思考も全部ログに残るAIのどっちが信頼できますかって議論になるか...
> [nishio](https://x.com/nishio/status/1883529721574785528) これを見ての反応(貼り忘れ)
>  >iriyak: これはきっと起きる。オペレーター（エージェント）が協調して仕事を分割して大きな悪事をなすみたいなシナリオを考えた時に追いかける方もきっと大変になるなぁ。 x.com/nishio/status/…
- [[思考プロセスが見れる]]

> [hrjn](https://x.com/hrjn/status/1883499625979719851) ウィルスはわからんけど、オペレーター向けの指示を埋め込むサードパーティJS（広告とか）だとかXSS的なやつとかはごまんとでそうな気はするな。


> [mizchi](https://x.com/mizchi/status/1883527824990171566) web2.0時代にAPIあればUI実装いらないよね的な話が無限にあったが結局[[課金モデル]]と噛み合わなくなってアプリで囲い込むようになったので、AI側の都合ではなく[[マイクロトランザクション]]の仕組み側が変わらないとそう簡単に変わらないと思っています


> [tokoroten](https://x.com/tokoroten/status/1883530250153521324) この後、「AIの操作は[[ロールバック]]可能なITシステム」ってのが要件になってきて、ITシステムの開発コストが爆増すると思ってる（もしくはそれを前提としたミドルウェアが開発される）
