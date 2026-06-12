---
title: "VSCode Remote ターミナル永続化"
---

2026-06-12
- 統合ターミナルの1タブ = 1 tmux にして永続化だけ tmux に任せてる
- 常時平行して3~8 Claude Codeが立ち上がっており、「重要なものほど上」と手で並び替えてタスクの管理をしている
- 人間は上から順に見て判断や入力をする
    - 完了したなら/clearして一番下に下げる
- limitで投げれないときとかに思いついたことも、入力欄に入れてタブを重要度順に並べている
- 残りlimitが少ない時、締め切りが近いとかの今やらないといけないタスクが上に移動し、トークンに余裕がある時でいいものは下に移動する

スクリプト: [vscode-tmux-tab](https://gist.github.com/nishio/815b90c837e1d70ebcb85ca94fd51e88)

何が起きているか（settings.json）
- "terminal.integrated.defaultProfile.linux": "tmux-tab"
    - VS Code でターミナルを新規に開くと、shell の代わりに毎回 /home/ubuntu/bin/vscode-tmux-tab が起動します。
    - tmux new-session … を直接書かずに自作スクリプトを噛ませているのがポイントです。
- VS Code側からは2つの変数だけ渡しています:
    - VSCODE_WORKSPACE_FOLDER = ワークスペースの絶対パス
    - VSCODE_WORKSPACE_BASENAME = その basename

なぜ記事の素の設定ではないのか
- 記事の new-session -A -s vscode-${workspaceFolderBasename} には罠があります。-A は「同名セッションがあればattach」なので、同じワークスペースで2つ目のタブを開くと1つ目と同じセッションにぶら下がる＝両タブが同じ画面のミラーになります。タブを分ける意味が薄れます。
- あなたのスクリプトはこれを避けて、タブごとに独立したセッションを作りつつ、ワークスペース単位でまとめる、という挙動にしています。

スクリプトの動作（行番号付き）
1. セッション名の prefix を決める（7-9行）
    - prefix = vscode-<basenameを安全化>-<絶対パスのsha1先頭8桁>
    - basename だけだと別の場所にある同名フォルダが衝突するので、絶対パスのハッシュを足して一意にしています。実際のセッション名は末尾に連番がついて vscode-mythos-ab12cd34-1, -2, … となります。
2. ロックを取る（11-15, 42-43行）
    - flock でワークスペース単位の排他ロック。VS Code 起動時に複数タブが同時復元されると、セッションの選定・採番が競合するので、その区間だけ直列化しています。
3. 再利用できる孤児セッションを探す（20-29行）
    - @vscode_claimed（claim 時刻）というユーザ定義オプションを各セッションに持たせていて、
        - 名前が prefix にマッチ
        - 誰も attach していない（session_attached == 0）
        - claim が空、または 30秒以上前
    - の条件に合うものがあれば、新規作成せずそれを再利用します。これは「VS Code 再起動／reload でタブが復元されたとき、前回のセッションを拾い直す」ための仕組みです。
4. 無ければ新規作成（31-38行）
    - 空いている連番を探して tmux new-session -d で作成。作業ディレクトリ -c はワークスペースに設定。
5. claim 印を押してロック解放、attach（40-48行）
    - 選んだセッションに現在時刻を @vscode_claimed として刻んでからロックを解放し、tmux -u attach-session で接続。-u は UTF-8強制。終了時に claim 印を消します。
- 関連する2つの設定
    - "terminal.integrated.enablePersistentSessions": true,
    - "terminal.integrated.persistentSessionReviveProcess": "onExitAndWindowClose"
    - これは VS Code 自身のターミナル復元機能。tmuxによる永続化と二重ですが、ウィンドウを閉じ直したときにタブ＝セッションの対応が復元されやすくなる方向に効きます。

- まとめ（一言で）
    - タブ1枚 = 独立した tmux セッション1個。ワークスペースごとに prefix でまとめ、VS Code 再起動時は flock + @vscode_claimed タイムスタンプで前回セッションを安全に拾い直す。
    - 記事の -A -s <basename> 方式（全タブ1セッション共有）の上位互換にあたる作りです。tmux は 3.6、~/.tmux.conf はマウスoff・クリップボード連携 off だけのミニマル構成です。




---
2026-06-09
[https://gist.github.com/nishio/85a7380a8567daf1760d5f8be5e12d85](https://gist.github.com/nishio/85a7380a8567daf1760d5f8be5e12d85)
[[VS Code Remote Development]] ターミナル永続化
[[tmux]]

<img src='https://scrapbox.io/api/pages/nishio/codex/icon' alt='codex.icon' height="19.5"/>
Remote側に以下を作成済みです。 /home/ubuntu/.vscode-server/data/Machine/settings.json
内容は、新規VS Code terminalを `/usr/bin/tmux new-session -A -s vscode-${workspaceFolderBasename}` で起動し、task/debug用terminalは通常の /bin/bash -l に逃がす設定です。JSON妥当性とtmux起動も確認済みです。
