---
title: "Mac Option Click Forces Selection"
---

Macの[[VSCode]]から[[VS Code Remote Development]]でリモート環境に入り、VSCodeのターミナルで[[Claude Code]]を使うシチュエーション
- デフォルトのシェルだと回線断でClaude Codeごと終了してしまうので[[tmux]]でセッションを永続化した
    - [[VSCode Remote ターミナル永続化]]

ところが、Claude Codeの出力した日本語をマウスで選択してコピーしたときに こんにちは → `ããã«ã¡ã¯` のように 化ける。
- このã やアクセント付き文字の羅列になる化け方は、UTF-8 のマルチバイト列が 1 バイトずつ Latin-1 として解釈された時に発生する典型文字化けパターン

ターミナルから文字をコピーする経路は大きく2つある
1. ネイティブ経路
    - ターミナルエミュレータ自身が画面の選択範囲を読み、OS クリップボードへ書く。 (VSCode なら「選択 → ⌘C / Ctrl+C」)。 ターミナルの内部バッファは正しいコードポイントを保持しているので、通常これは UTF-8 で正常に動く。
2. [[OSC 52]] 経路
    - ターミナル内で動くアプリが エスケープシーケンス OSC 52 を送り、選択内容を base64 でクリップボードへ"押し込む"。
    - リモート越しでもアプリ側からクリップボードを操作できる便利な仕組みだが、 この base64 のエンコード/デコードで UTF-8 を Latin-1 として扱う実装バグが一部のターミナルにあり、 そこで化ける。
    - VSCodeのターミナルにこのバグがあるっぽい

一部のテキストユーザインターフェイス(TUI)で動くアプリは自前でマウストラッキングをする
- tmuxの`mouse-mode`がONの場合など
    - Claude Code も、fullscreen rendering が有効な場合、terminal mouse events / mouse capture を使う。
- これらのアプリで画面をドラッグ選択した場合に、選択がネイティブ選択にならず、コピーがOSC 52 経路に乗る。
- 素のbashなどではこの挙動をしないので "tmuxにしたら化けるようになった" という体験として観測される

VS Code + macOS なら Terminal › Integrated: Mac Option Click Forces Selection をONにしたうえで Option+drag すると、リモートにマウスイベントを送ってTUIのmouse-modeで選択するのではなく、手元側でネイティブの選択が行われる
- なのでその状態でCmd+Cすれば文字化けせずにコピーできる
- VSCodeの Terminal > Integrated: Copy on Selection をONにすれば、選択した時点でコピーされるので便利
