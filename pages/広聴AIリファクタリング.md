---
title: "広聴AIリファクタリング"
---

6月のリリース
[https://gist.github.com/nishio/0a1812750627620ff6ede948f13c993b](https://gist.github.com/nishio/0a1812750627620ff6ede948f13c993b)

2026-01-19
腰を据えて作業をする
- [[40Hz刺激]]と[[ポモドーロタイマー]]を回して集中力高く取り組みたい
- 片手間で「AIエージェントでどこまでできるか試す」とかやってると人間の集中力と理解力が不足して技術的負債が溜まる

<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>Phase 0: 現状把握・棚卸し
- エントリポイントとビルド経路の整理（docker compose / Makefile / scripts）。
- 既存レポート結果JSONの契約を確定。
- client/admin間の重複UIの洗い出し。

ポートやステップ、出力の型などを明確化

[https://github.com/digitaldemocracy2030/kouchou-ai/blob/refactoring/docs/refactoring/phase0_investigation.md](https://github.com/digitaldemocracy2030/kouchou-ai/blob/refactoring/docs/refactoring/phase0_investigation.md)

Step 1
配置の変更
- この機会にserverとかclientとかのよくわからない名前も整理したい気がする
- apps/client → apps/public-viewer
- apps/client-static → apps/static-site-builder
- 従来の名前との対応づけのドキュメントもあるべきだな

新名 と Docker サービス名 が異なっているのは不必要に複雑さを増していると思う
- <img src='https://scrapbox.io/api/pages/nishio/Claude/icon' alt='Claude.icon' height="19.5"/>Docker サービス名も統一する（推奨）
    - メリット: 名前が一貫してわかりやすい
    - デメリット: Azure Container Apps名も変更が必要（Azureリソースの再作成が必要になる可能性）
- なるほどね<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
    - ここは変更して綺麗にする方がいいだろう

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>Docker サービス名とAzure Container Apps 名の変更に伴う互換性の失われポイント、すでにデプロイしている人が何に気をつける必要があるかをドキュメントに加筆して。
- →[https://github.com/digitaldemocracy2030/kouchou-ai/blob/refactoring/docs/refactoring/naming_convention.md](https://github.com/digitaldemocracy2030/kouchou-ai/blob/refactoring/docs/refactoring/naming_convention.md)
🍅

ついでにCodexもチャットモードで起動して作業をレビューさせることにした
- 人間とCodexの二馬力レビュー

<img src='https://scrapbox.io/api/pages/nishio/Claude/icon' alt='Claude.icon' height="19.5"/>ワークスペースが必要な理由:
- 型定義の共有 - apps/public-viewer/type.ts と apps/admin/type.d.ts に同じ型定義（Meta, Report, Argument, Cluster等）が重複していた。@kouchou-ai/report-schema パッケージを作り、両アプリから workspace:* で参照することで重複を解消。
- 依存関係の効率化 - ルートで pnpm install 1回で全パッケージの依存関係をインストール。共通の依存関係（React, Chakra UI等）は自動的に重複排除される。
- 将来のUI共有 - packages/ui-shared/ として共通UIコンポーネント（button, dialog等）を切り出す準備。現在12個のファイルが重複しているが、themeへの依存があるため段階的に対応予定。
- 一貫したコマンド実行 - pnpm -r で全パッケージへの一括操作、pnpm --filter で特定パッケージへの操作が可能。
今は@kouchou-ai/report-schemaの型をまだインポートしていませんが、Phase 4-5で各アプリの型参照を移行する際に活用します。 report-schemaパッケージのビルドを確認します。

Phase 1完了
- テストをしよう
- テストは通った(もちろんテストのカバーが完璧かというとそうではないわけだが)
- Phase 2に進もう
    - ここから分析のコア部分の抽出

🍅

AIエージェントの作業待ちの時に他のプロジェクトに移動しない縛り

12:16 <img src='https://scrapbox.io/api/pages/nishio/Claude/icon' alt='Claude.icon' height="19.5"/>残りのPhase 2作業は約2-3時間程度かかります。 続けますか？
- AIの作業を眺めながら昼食
- ![image](https://gyazo.com/347a17244dcc8fbe1140a636b1e680c5/thumb/1000)

> """Cluster the arguments using UMAP + HDBSCAN and GPT-4."""
- おや、これは事実に反するな
    - 後で確認

12:31に一旦終わったけど「localにPython3.12がないからテストをスキップするね」と舐めたことを言ってるからPython3.12をインストールして試せとツッコミを入れる

待ち時間に他のプロジェクトに手を出さないという強い気持ち

12:57 あらためてPhase 2完了
- このタイミングでCodexの側のレビュー修正を反映する
- 待ってる間にClaude Codeの側はcompactするか
- > Codexの側のレビュー修正を反映する
    - 思った以上に時間がかかっている(13:17)
        - Thinking effortを最大にしたままだったw

> プロンプトはAPIから設定として渡されることが判明しました。report_launcher.py が report_input.prompt からプロンプトを取得して設定に含めています。 Phase 2.5.4はN/A（該当なし）です。APIがプロンプトを提供するため、パッケージにプロンプトファイルを含める必要はありません。CLIでプロンプトなしで使う場合のフォールバックは将来必要に応じて追加します。 次のPhase 2.5.5（apps/api統合）に進みます。
うーん、デフォルトプロンプトを使うべきだね

pipをinstallして適当なCSVを分析して、結果を受け取ってmatplotlibで可視化する

---

CLI実行、PyPIからのインストール、プラグイン拡張などを可能にするリファクタリング計画を実行中です(年末に話していたもの)
- 前2つは動作確認済み
    - CLIで分析処理が可能になりました
        - [https://github.com/digitaldemocracy2030/kouchou-ai/blob/refactoring/docs/CLI_QUICKSTART.md](https://github.com/digitaldemocracy2030/kouchou-ai/blob/refactoring/docs/CLI_QUICKSTART.md)
    - Pythonスクリプトからimportして使うことも可能です
        - [https://github.com/digitaldemocracy2030/kouchou-ai/blob/refactoring/docs/IMPORT_QUICKSTART.md](https://github.com/digitaldemocracy2030/kouchou-ai/blob/refactoring/docs/IMPORT_QUICKSTART.md)
- プラグイン拡張機能は実装済みだがまだ実際に差し替えるプラグインがないので試していない
    - 従来通りの分析も各ステップがプラグインに変わっているが、問題なく通して実行できることを確認済み
    - プラグイン作成ガイド
        - [https://github.com/digitaldemocracy2030/kouchou-ai/blob/refactoring/docs/PLUGIN_GUIDE.md](https://github.com/digitaldemocracy2030/kouchou-ai/blob/refactoring/docs/PLUGIN_GUIDE.md)
- リファクタリングと言っておきながら破壊的更新が入っています、すみません
    - [https://github.com/digitaldemocracy2030/kouchou-ai/blob/refactoring/docs/refactoring/naming_convention.md](https://github.com/digitaldemocracy2030/kouchou-ai/blob/refactoring/docs/refactoring/naming_convention.md)
    - pathがserverでDocker名がapiだとか、clientという名前のサーバを建てる必要があるとかの「混乱を招くネーミング」がこの機会にまとめて修正されています
- pipはどういう形？
    - pipだけ別のrepoに分かれてはいない
    - ここがpipの定義[https://github.com/digitaldemocracy2030/kouchou-ai/blob/refactoring/packages/analysis-core/pyproject.toml](https://github.com/digitaldemocracy2030/kouchou-ai/blob/refactoring/packages/analysis-core/pyproject.toml)
    - まだ0.1.0でとりあえずできた状態
        - どうアップデートしていくかはあとあと考える
        - 将来的にはrepo secretにtokenをおいてこのfolder以下が更新されたら自動更新するか？
        - 自動更新とかしなくてもバージョン番号を振ってリリースするときに一緒にやるのでいいのでは


---
非エンジニア向けUX:
- YouTube URL を貼る
- 「レポート生成」クリック
- 待つ
- JSON/レポート閲覧

Day 2
- Day 1の後半は夕食や会議で集中力が途切れて、そうなると「よく理解しないままAIに先に進ませる」をやってしまってよくない
- 寝て起きてクリアになった脳で「これってなんのために必要なんだっけ？」と質問した

プラグインの仕組み
- 色々な機能を追加したい v.s. 使わない人にまでデフォルトでONにしたくない
- pluginがどういう設定を必要とするかはコードで管理され、設定不良で実行された場合にはなるべく早い段階で警告したい

OSSとして、機能追加を気軽にどんどんできるのが好ましい
- が、どんどん受け入れると依存関係が大きくなっていき、セットアップの時間や失敗確率などの形でデメリットが出てくる
- プラグインという形にし、境界を明確にする
- 色々な機能を追加したい v.s. 使わない人にまでデフォルトでONにしたくない
    - 使いたい機能をプラグイン単位でON/OFFすべき
- 設定ファイルがどんどん大きくなって混乱
    - どのプラグインがどの設定を必要とするのかをコードで記述すべき
    - 設定不良で実行された場合にはなるべく早い段階でわかりやすく警告したい

2025年12月6日 | 広聴AIの方向性について
- [https://docs.google.com/document/d/1GRHgFn0J4OGyaBd8lcWPEKmjPr2Kjwl2xpzc_i21AuU/edit?tab=t.0](https://docs.google.com/document/d/1GRHgFn0J4OGyaBd8lcWPEKmjPr2Kjwl2xpzc_i21AuU/edit?tab=t.0)
2025年12月13日 | 広聴AIの方向性について2
- [https://docs.google.com/document/d/16GMzidgqtxxdIyUnlEsgiAS5j73bd2iAaSgYMMhoSoM/edit?tab=t.0](https://docs.google.com/document/d/16GMzidgqtxxdIyUnlEsgiAS5j73bd2iAaSgYMMhoSoM/edit?tab=t.0)




入力プラグイン・分析プラグイン・可視化プラグイン
- ![image](https://gyazo.com/70860ea3e16aeb0b87de0d17ebd32a7b/thumb/1000)

![image](https://gyazo.com/76c20716f55e08cbd198343495ef0b42/thumb/1000)
![image](https://gyazo.com/d81e48795be0e67f5292b7b4ab61541b/thumb/1000)
![image](https://gyazo.com/487e10522ea2ab6bdef647af1998fbd3/thumb/1000)
みためはいいんだけどね
- 「プラグインはコード上で明確に分かれていて、類似のプラグインを作る人が容易に真似をできるのが好ましい」という要件をAdmin UIまで含めて考えた時に満たしているか？
- Adminのコードに書き込んでる気がするのでapi以下とadmin以下に分散してるよな
    - そんなことなかった

---
プラグインには入力プラグイン、分析プラグイン、可視化プラグインの3通りがある
- 次は可視化プラグイン

![image](https://gyazo.com/af56999b44a99ee8e1497158086cdabe/thumb/1000)![image](https://gyazo.com/43ddac15c0ab52f89a54eb60512a9832/thumb/1000)


どの分析がデータに何を要求していて、何を供給するのか
- どの可視化がデータに何を要求するのか

---
Claude Max(x5)なのに
> Limit reached · resets 7pm (Asia/Tokyo) · /upgrade to Max 20x or turn on /extra-usage

今は「可視化プラグインの選択」を更新する機能を追加したが、未テスト

![image](https://gyazo.com/c64e5a85eb9cf5bba0ab80b32b886781/thumb/1000)
done

予定していた作業完了

あなたはレビュワーです。refactoringブランチに入ってからの全ての修正に関して、まずpatchなどに出力し、それから頭から順に読んでおかしなところがあればREVIEW.mdに書いて。必要に応じて関連したソースコードを調査することは良いことです。あなたが実装の修正をする必要ありません。全部レビューしたら教えて。そのREVIEW.mdを実装者に渡して修正します。

2026-01-21
[「レポートの取得に失敗しました」を親切にする · Issue #749 · digitaldemocracy2030/kouchou-ai](https://github.com/digitaldemocracy2030/kouchou-ai/issues/749)


通したユーザ体験のテストをする
- Docker Desktopをupdateする


![image](https://gyazo.com/b2e593600396d75c3259395a2f8677f7/thumb/1000)

[https://www.youtube.com/watch?v=ZGHbKWGgH_E](https://www.youtube.com/watch?v=ZGHbKWGgH_E)


