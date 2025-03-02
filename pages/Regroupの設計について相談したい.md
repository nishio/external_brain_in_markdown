---
title: "Regroupの設計について相談したい"
---

- 何について相談したいのか明確ではない状態からとりあえず書き出していった
- 書き出しただけで相談する前に解決しちゃった、と思ったが、相談したら意外と事前にはイマイチだと思ってスルーしてた解決法が一番マシなのではないかと気づいた
- 具体的には
    - 平行移動をキーボードで行うという案について、気づいてはいたが、無意識に無視していた [[Regroupの設計について相談したい#6077ff00aff09e00008ebf98]]
        - 振り返って考えると無意識にiPadで使う時のことを考えててキーボードを繋ぐのはありえないと考えていた
    - 「平行移動について他に何かあるか？」で「PCでの操作が不便」、「何が価値？」で「ストレスなく操作できるとよい」が明確になった
    - 「PCでストレスなく操作する」ために「何が起こる必要があるか」を考えて、シフトドラッグはキーボードとポインティングデバイスの両方を使うわけだからむしろキーボードだけで完結する方がストレス少ないのではと気づいた

<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>あなたはこの会話で何がどうなるとよいのでしょう？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>Regroupの設計について相談したい
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>その「Regroup」は、どんな「Regroup」ですか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>まず聞いて
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>はい
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>Regroupは元々、iPadで二本指ジェスチャーで拡大縮小平行移動をすることを前提として作られた。電子的KJ法をやるにあたってコンピュータの画面は狭すぎるってことがそもそもの課題であり、それをスムーズな拡大縮小で解決できるのではないか、が仮説であった
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>「Regroup」
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>開発する際にMacbookを使うのでMacbookでも一通りの操作はできた方が都合がいい、そこで二本指での上下で拡大縮小になった、これはホイールイベントに変換される。Macbookではないユーザはホイールのついているマウスを使うか、シフトドラッグをすることになる。
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>「拡大縮小」
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>iPadでの拡大縮小はGoogleマップと同じように「今レンダリングしている内容を画像として拡大縮小、操作完了後に再レンダリング」という仕組み。しかしホイールイベントには明示的な終了がないのでこの方法は使えなかった。あくまでホイールイベントの到着ごとにズームの値を調整することしかしていない。そもそもPC上での操作はデバッグ目的のつもりだった。
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>「拡大縮小」
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>Keicho-Regroup連携のチュートリアルを作ろうとしていて、そもそもユーザがiPadを持っていると想定するのは難しいのでPCでも使える必要があると考えた。(今気づいたけどそもそも半数のユーザがスマホから使っててそのままスマホの小さい画面でRegroupを開いちゃうから、大きい画面で開くようにアドバイスする必要があるな、これは今回の本題ではないが)
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>「Regroup」
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>で、実際にPC上で使ってみると不便に感じるからどうしたらいいかなぁ、というのが相談したかった。相談する前は「モード切り替えボタンを押すのが面倒だからホットキーがあるといい？」「全体が見えるところまでズームアウトするキーがあるといい？」と思っていたが、話していて思ったこととしては拡大縮小の実装がそもそもあんまりきちんと考えられてない。
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>「拡大縮小」
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>理想としてはiPadと同じ二本指ジェスチャーになることだけど、ブラウザアプリがキャプチャできない可能性が高い。Macbookでない人が使えない問題も残る。iPadで解決されててPCで解決されてない問題は実は平行移動だ。
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>「iPad」
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>iPadでは拡大縮小も平行移動も二本指ジェスチャーなので、投げ縄選択モードでもモード切り替えなしに使うことができる。一方でMacbookではモードを切り替えて使っていた。むしろ「モードを切り替えずに使える」という意味ではシフトドラッグが適切だが、使ってなかった。
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>「拡大縮小」
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>実装過程で「平行移動モード」が真っ先に作られて、これが今でもデフォルトのモードになってる。このモードは付箋をドラッグすると付箋が動き、画面をドラッグすると平行移動。だけどその後、複数まとめて移動したくて投げ縄モードがつき、1枚だけ動かす時にモードを切り替えるのも馬鹿らしいので投げ縄モードで1枚付箋の移動ができるようになった。もはやPCでの平行移動の時にしか使われないモードになっている。
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>「平行移動」
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>モードを切り替えずに視点の平行移動をするって方法としては、キーボードで移動する手と、ミニマップを作る手がある。ミニマップができるといいが、描画のコストがどれくらい上がるか未知数。
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>「平行移動」
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>平行移動モードをなくすという点では「うっかり操作して壊すのが怖い」という人がいるので、デフォルトは編集をしないモードになれば良い。
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>「平行移動」
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>なんか掘り下げ質問を使う前に結論が出てしまったが、僕のネクストアクションは「平行移動モードへのモード切り替えを禁止して使ってみて不満点を洗い出す」な気がした
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>「平行移動」
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>おしまい
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>あなたはこの会話で何が起きて欲しいですか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>現状の漠然とした問題意識が明確になって、ネクストアクションが定まるとよかった
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>
- >  なんか掘り下げ質問を使う前に結論が出てしまったが、僕のネクストアクションは「平行移動モードはのモード切り替えを禁止して使ってみて不満点を洗い出す」な気がした
- この「平行移動」は、どんな「平行移動」ですか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>マップ上の色々なところを見るために視点を動かすこと
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>
- >  なんか掘り下げ質問を使う前に結論が出てしまったが、僕のネクストアクションは「平行移動モードはのモード切り替えを禁止して使ってみて不満点を洗い出す」な気がした
- この「平行移動」について、他に何かありますか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>PCでそれをやることに不便を感じていた
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>あなたが価値を感じているのは何ですか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>ストレスなく操作できて付箋の整理ができるといい
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>
- >  なんか掘り下げ質問を使う前に結論が出てしまったが、僕のネクストアクションは「平行移動モードはのモード切り替えを禁止して使ってみて不満点を洗い出す」な気がした
- あなたはこの「平行移動」をどう知るのですか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>自分でもシフトドラッグの機能を忘れてた、ユーザも当然わからないのでガイドが必要
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>
- >  なんか掘り下げ質問を使う前に結論が出てしまったが、僕のネクストアクションは「平行移動モードはのモード切り替えを禁止して使ってみて不満点を洗い出す」な気がした
- この「平行移動」に関して、何が起こるとよいですか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>ストレスなく直感的に操作できるといい
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>それには「平行移動」に何が起こる必要がありますか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>少なくともモード切り替えを要求するのはダメだ。シフトキーを押させるのも割と微妙。キーボード操作はゲームなどでなれてる人も多いからそういうものだと割り切ることもできるかもしれない。ミニマップも視点を切り替えるという意味では明示的だが、カーソルをミニマップに移動して、よくみてクリックする必要がある。そう考えると意外とキーボードでの平行移動が一番有望かも？
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>「平行移動」に関して、それができますか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>その機能を試しにつけてみることはできる
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>
- >  少なくともモード切り替えを要求するのはダメだ。シフトキーを押させるのも割と微妙。キーボード操作はゲームなどでなれてる人も多いからそういうものだと割り切ることもできるかもしれない。ミニマップも視点を切り替えるという意味では明示的だが、カーソルをミニマップに移動して、よくみてクリックする必要がある。そう考えると意外とキーボードでの平行移動が一番有望かも？
- この「平行移動」は、どこから来るのですか？

[https://keicho.netlify.app/#talk=LrTDWXVO1l9BjNPIOfI6](https://keicho.netlify.app/#talk=LrTDWXVO1l9BjNPIOfI6)