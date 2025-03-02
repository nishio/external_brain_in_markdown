---
title: "Talk to the City Turbo試す"
---

prev [[Talk to the City試す]]

[https://talktothecity.org/report/tset-report-for-nishio](https://talktothecity.org/report/tset-report-for-nishio)

![image](https://gyazo.com/d3f861565fbe98a48aea59ceb746ed7c/thumb/1000)
![image](https://gyazo.com/391f0ebb6b6c0f335c23b20b2ec36cfa/thumb/1000)
![image](https://gyazo.com/6f66a77ed0e8eb5e37a435785773e4d5/thumb/1000)

ドキュメントを見る
- [https://talktothecity.org/docs](https://talktothecity.org/docs)
- 技術的なスキルがなくても使えるよ！と書いてる
- 拡大した状態でどうやってスクロールするのかわからなくてつまずいてる
- は？エディターの説明はどこ？
- [https://talktothecity.org/docs/ai-pipe-guide](https://talktothecity.org/docs/ai-pipe-guide)
- <img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>パン (スクロール): 背景をクリックしてドラッグすることで、表示領域を移動(パン)できます。
    - いや、選択モードの箱が出るんだけど？
    - リロードしたらドラッグで動くようになった！バグ？

![image](https://gyazo.com/a8ae0cd8c048ff3e350d11d6d707e01f/thumb/1000)
- トピックの個数を変えたいとする
- 右上の設定ボタンを押す
- ![image](https://gyazo.com/6e677341d44be4ec9d36f08f20483f57/thumb/1000)
    - 箱が画面外まで広がった！
    - この状態でノードをドラッグしたら動くが、背景をドラッグしたら範囲選択になる
        - バグだろ、これ
    - ![image](https://gyazo.com/d791310b6393010a0238622874e6af5d/thumb/1000)
        - 結局設定できないじゃん？
    - なおズームアウトはできなくなった...

![image](https://gyazo.com/ebff07c9bb245660bc2971231ad2611d/thumb/1000)
- ホバーしないと説明が読めないUI、なお画面外に出るのでホバーしても読めない
- ノードのマニュアル
    - [https://talktothecity.org/docs/nodes](https://talktothecity.org/docs/nodes)
        - ABC順なので名前がわからないと探せない...

Pinecore使わなくてもPinecoreのAPIを要求される
- 36文字の適当なものをいれればいい

自動保存されるものとそうでないものがある
- パラメータは自動保存でノードの接続関係は手動セーブかな

画面を拡大したり縮小したりして編集してるうちにUIがどっかに言って保存ボタンを押せなくなる、は？
- もう視力があんまりよくないからUIにちっちゃい字で表示されるとか嫌なんだけど？


TTTC Turboを使ってみて
- いやこれ同じTTTCって名前だけども今使ってるTTTC Scatterとはアルゴリズムまったく違いますよね
- LLMにデータを突っ込んで「トピックとサブトピックを作れ」をやった後で抽出フェーズで「抽出し、トピックとサブトピックに割り当てろ」をやってる
- 散布図は出ないんだ？Node一覧にないよね。
