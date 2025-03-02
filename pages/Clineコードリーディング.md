---
title: "Clineコードリーディング"
---

[https://github.com/cline/cline](https://github.com/cline/cline)
private [https://chatgpt.com/c/677f734a-45f8-8011-9dec-69a03aa86473](https://chatgpt.com/c/677f734a-45f8-8011-9dec-69a03aa86473)
<img src='https://scrapbox.io/api/pages/nishio/o1 Pro/icon' alt='o1 Pro.icon' height="19.5"/>
- このコード一式は、VSCode拡張のWebviewで動くReactアプリが、実際の開発作業(ファイル操作・コマンド実行など)を“AIエージェント”に行わせるためのUIロジックをまとめたものです。VSCode拡張本体と、このWebview内のReactとの間でメッセージをやり取りして、実際の操作(例: ファイル編集、コマンド実行、ブラウザ操作など)を可能にしています。以下、もう少し詳しく「どのような流れ・仕組みでロジックを実行しているか」を説明します。

1. ChatView でのロジックフロー
    - 1-1. ユーザー入力（テキスト＆画像）のハンドリング
        - ChatTextArea コンポーネントでユーザーが入力し、送信すると、以下のような処理が走ります。
            - テキストや画像データをまとめて vscode.postMessage({ type: "newTask", ... }) もしくは askResponse として拡張機能側に送る（ChatView内の handleSendMessage やボタン押下時の handlePrimaryButtonClick 等）。
            - これを受け取った拡張機能側が、AIエージェントとのやりとりを開始・継続。
    - 1-2. 拡張機能からのメッセージ受信と描画更新
        - Webview側(App.tsx / ChatView)は useEvent("message", ...) 等でメッセージを待ち受けており、
            - APIリクエスト開始 (api_req_started),
            - ツール使用(ファイル編集等) (tool),
            - コマンド実行 (command),
            - ブラウザ操作 (browser_action),
            - 最終結果 (completion_result)
        - といった情報が届いたら React の state (clineMessages など)を更新します。
        - 更新された state に応じて、ChatRow や BrowserSessionRow コンポーネントがリスト描画され、UIに反映されます。
        - たとえば api_req_started が来た段階ではローディング表示を出し、api_req_failed やコスト情報の付いた api_req_started（再送されるメッセージ）を受け取ったら“完了”に切り替える、などが行われています。

    - 1-3. “タスク”の概念と承認(Approve/Reject)フロー
        - 1つの大きなタスクの中で、AIが「ファイルを編集したい」「コマンドを実行したい」「ブラウザを使いたい」といったアクションを“提案”してくる (= ask メッセージ)。
        - これらを受け取った時、ChatView は「承認ボタン / 却下ボタン」などを表示し、ユーザーに許可を求めます。
        - ボタン押下時に askResponse を拡張機能へ送信して、承認or拒否に応じた処理がVSCode拡張側で実行されます。
        - “Mistake limit”や“auto approval limit”に引っかかった場合は「このまま続行するか、新しいタスクを始めるか」等をユーザーに選ばせるロジックも同様に実装されており、メッセージ種別(ask = "mistake_limit_reached" など)をもとに画面を分岐しています。

2. ファイル操作やコマンド実行の内部ロジック
- 2-1. ツール(例えば tool = "editedExistingFile") の流れ
    - AIが「ファイルをこう編集する」という指示(差分や新規ファイルの中身など)を ask: "tool" や say: "tool" として渡してくる。
    - ChatRow 側は tool.tool の値を判定して、editedExistingFile / newFileCreated / readFile / searchFiles などに応じたUIを表示。
    - 承認が必要なときはボタンを出し、クリックで askResponse を送信。
    - 承認されたら拡張機能本体がVSCode APIを通じて実際のファイル編集を行う（あるいは却下なら何もしない）。
- 2-2. コマンド実行( command )
    - AIが「ターミナルでこのコマンドを実行したい」というメッセージを送る。
    - UI上ではChatRow でコマンド＆出力が表示され、承認ボタンが押されると拡張機能本体のターミナル(or Shell)でコマンド実行する仕組み。
    - 実行中の標準出力／標準エラー出力が再び api_req_started→command_output の形で部分的に返ってくる場合もあり、それを反映してリアルタイム出力に書き足す、といった処理が行われる。
- 2-3. ブラウザ操作( browser_action )
    - BrowserSessionRow の仕組みを使い、AIが「特定サイトにアクセス」「クリック」「スクロール」などのアクションを逐次提案。
    - 承認で進めると、拡張機能本体がヘッドレスブラウザなどを制御してキャプチャ・テキストを取得し、再度Webviewに “スクリーンショット付き” の結果メッセージを送ってUI更新する。

3. state管理やコンテキスト(ExtensionStateContext)の役割
- 3-1. 全拡張機能状態の一元管理
    - ExtensionStateContext が拡張機能で保持している状態(ExtensionState)をReactのContextとして包み、どのコンポーネントからでも useExtensionState() で読み書きできる形にしている。
    - たとえば
        - 選択したAPIプロバイダやモデルID (apiConfiguration)
        - 過去のタスク履歴(taskHistory)
        - テーマ情報(theme)
        - MCP関連サーバー一覧(mcpServers)
    - などがここに集約されている。
- 3-2. メッセージごとの分岐
    - React側(handleMessage)でメッセージを受信→switch (message.type) で state, theme, workspaceUpdated, partialMessage, openRouterModels, mcpServers …などを場合分けし、それぞれ setState(...) や setMcpServers(...) のように更新している。
    - こうして更新されたContext stateが ChatView や SettingsView 等に伝わり、UIをリフレッシュする。

4. 履歴管理やチェックポイント
- 4-1. HistoryView
    - 過去のタスク(taskHistory)を検索表示するコンポーネント。
        - Fuse.js を使い検索（Fuzzy search）し、絞り込み＆ソート可能。
        - 選んだタスクIDを vscode.postMessage({ type: "showTaskWithId", ... }) して再表示できる。
- 4-2. Checkpoints (差分比較・復元)
    - 途中経過ごとにワークスペースをGitなどでスナップショットしておき、CheckpointControls のボタンから 「この時点の差分を見る」「この時点に復元する」 といった操作が可能。
    - ボタン押下で checkpointDiff / checkpointRestore メッセージを拡張機能に投げ、それを受けた拡張機能が Git の差分や元に戻す操作を行うロジック。

5. MCP (Model Context Protocol) サーバー拡張機能
- 5-1. MCPサーバーの接続一覧
    - McpView コンポーネントで表示。
    - MCPサーバー（ローカルにある追加ツール提供サーバー）を拡張機能が起動・接続し、そのステータスや提供ツールをここで参照可能。
    - AIが “use_mcp_server” を使って外部リソースやツールを呼ぶときも、承認UIが出てくる。
- 5-2. McpToolRow, McpResourceRow でツール／リソースをリスト表示
    - “execute_command”等のツールが登録されていれば、AIが動的に利用できる。
    - VSCode側がサーバー起動コマンドや接続先を管理し、エラーがあれば再接続ボタン等を押せる仕組み。

まとめ
- AIの提案(Ask)→承認/却下→実行結果(Say)を順々に受け取りながら、VSCode拡張が実ファイル・コマンド・ブラウザ・追加ツールなどをコントロールするのが中心の流れ。
- React側ではコンテキストで状態を一元管理しつつ、メッセージを受け取るたびに適切なUIを更新する。ユーザーがUI操作を行ったら postMessage で拡張機能へ応答を送り、処理が進行する。
- 大きくは「チャット(メッセージの流れ)」「ファイル操作・コマンド実行」「履歴・チェックポイント」「MCPツール管理」などが、それぞれ Reactコンポーネントを通じて実現されている、という仕組みになっています。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>このコードの具体的にツールを実行しているところはどこ？
(Cline)
src/core/Cline.tsファイルには、ツールを実行するためのロジックが含まれています。特に、以下のメソッドがツールの実行に関連しています。
- executeCommandTool メソッド (行1069-1144):
    - このメソッドは、コマンドを実行するためのツールを提供します。ターミナルを管理し、コマンドの出力を処理します。
- presentAssistantMessage メソッド (行1271-2691):
    - このメソッドは、アシスタントメッセージを処理し、ツールの使用を管理します。特に、tool_use ブロックを処理する部分で、ツールの実行が行われます。
- recursivelyMakeClineRequests メソッド (行2693-3007):
    - このメソッドは、ユーザーからのリクエストを再帰的に処理し、ツールの使用を含むAPIリクエストを行います。
これらのメソッドは、ツールの実行に直接関与しており、特にtool_useブロックを処理する際にツールを実行します。


LSPを使ってるかなという質問に対して
<img src='https://scrapbox.io/api/pages/nishio/o1 Pro/icon' alt='o1 Pro.icon' height="19.5"/>
このコード一式を見る限り、Language Server Protocol (LSP) を直接利用してはいません。例えば「LSPクライアントを起動してコード解析結果を取得」「hoverやcompletionなどの LSP 通信」を行うようなコードは含まれておらず、代わりに以下のような方法で情報をやり取りしています。

ファイルやディレクトリの情報
- listFilesTopLevel や listFilesRecursive といったツール呼び出しがあり、VSCode側のAPIやファイルシステムAPIを使ってディレクトリ一覧やファイル内容を直接取得しています。

差分(differences)の取得
- Gitなどで管理しているスナップショット(“Checkpoints”)に対して、拡張機能本体がdiffを計算し、Webviewに送り返す仕組みを取っています。
- LSPによるコード差分の計算ではなく、Git などのバージョン管理情報を活用しているイメージです。

検索や“定義一覧の抽出”
- searchFiles や listCodeDefinitionNames で正規表現検索またはテキストベースの解析を行う記述が登場しますが、これもLSPではなく拡張機能サイドで直接ファイルのテキストを読み込み、正規表現マッチさせるなどして情報を返しています。

コマンド実行やブラウザ操作
- ターミナルコマンドを実行したり、ヘッドレスブラウザ操作したりする際の情報は、Language Server Protocol は経由していません。
- 拡張機能本体とWebview間の独自メッセージ (api_req_started, command, browser_action など) でやり取りしており、LSPとは無関係です。

LSPを用いたコード補完やシンボル情報取得はしていない
本コードはAIエージェントの操作（ファイル読み書きやコマンド・ブラウザ操作など）をVSCode拡張の機能で行う目的で書かれており、LSPによりASTを解析したりコード補完情報を取得したりしている形跡はありません。従って、Language Server Protocol で得られるような型情報やリファレンス情報、診断(警告・エラー)などは扱っていない、というのが結論です。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>自前でASTを作って定義情報を取得したりしている
