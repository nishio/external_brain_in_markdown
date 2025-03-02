---
title: "pVecSearch2024-03-22振り返り"
---

[/plurality-japanese/ベクトル検索の改善](https://scrapbox.io/plurality-japanese/ベクトル検索の改善)

<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>pVectorSearchプロジェクトのまとめを作成しました。

[[pVectorSearch]]
- このScrapboxを中心とする[[ベクトル検索]]に関するプロジェクト
- [[西尾のベクトル検索]]の開発や実験、考察が含まれる

開発の進捗
- 2023年4月29日~5月31日 ([[pVectorSearch2023-04-29~05-31]])
    - このScrapboxの[[ベクトル検索]]に関する初期の考察
    - まずはAPIを作ることを構想 (自分用の道具として)
- 2023年6月2日~5日 ([[pVectorSearch2023-06-02]], [[pVectorSearch2023-06-05]])
    - ローカルのDockerで[[qdrant]]を建てて色々実験
    - [[Scrapbox ChatGPT Connector]]の知見を応用
    - 検索してヒットしたテキストとページを表示
    - [[埋め込みAPI呼び出しの並列化]]を検討
- 2023年6月6日 ([[pVectorSearch2023-06-06]])
    - 管理機能の実装 (検索クエリの保存、パーマリンク生成)
    - 公開、[[西尾のベクトル検索]]リリース
- 2023年6月7日 ([[pVectorSearch2023-06-07]])
    - 他の人のScrapbox ([/halsk](https://scrapbox.io/halsk), [/yuiseki](https://scrapbox.io/yuiseki), [/tkgshn](https://scrapbox.io/tkgshn)) もクロール
    - 複数人のScrapboxを横断検索できるようになる
- 2023年6月13日~15日 ([[pVectorSearch2023-06-13]], [[日記2023-06-15]])
    - [[非公開資料をベクトル検索対象にする]]ことを検討
    - [[蔵書横断ベクトル検索]]のための情報の単位について考察
- 2023年6月27日 Omoikane Embed([/omoikane/Omoikane Embed](https://scrapbox.io/omoikane/Omoikane Embed))
    - [[Democratic Inputs to AI]]のためのフォーラムに導入
    - 概要:
        - Scrapboxのコンテンツを自動的にベクトル化してインデックスを作成するシステム
            - 追加でNotionからもデータを採集
        - Github Actionsを使って毎日朝6時に自動実行
        - 500トークンごとに分割してOpenAIのEmbedding APIでベクトル化
        - Qdrantデータベースにアップロードしベクトル検索に利用
    - Ver1: 6/29 [https://github.com/nishio/omoikane-embed/tree/v1.0](https://github.com/nishio/omoikane-embed/tree/v1.0)
        - 毎日実行されるようになった
    - 7/23 [/omoikane/作業メモ:Omoikane Embedを他のプロジェクトに入れる](https://scrapbox.io/omoikane/作業メモ:Omoikane Embedを他のプロジェクトに入れる)
    - Ver2: 7/29 [https://github.com/nishio/omoikane-embed/tree/v2.0](https://github.com/nishio/omoikane-embed/tree/v2.0)
        - Scrapboxにレポートを書くようになった
        - 関連: [[omni]]
    - 2023/8/9
        - コードを整理して他のプロジェクトに入れやすくした
        - [/omoikane/Omoikane Embedを他のプロジェクトに入れるには](https://scrapbox.io/omoikane/Omoikane Embedを他のプロジェクトに入れるには)
- 2023-09-22 Scrapboxにレポートを書くomniはprivate projectに移動した
- 2023-10-17 Plurality Vector Search released([/plurality-japanese/Plurality Vector Search](https://scrapbox.io/plurality-japanese/Plurality Vector Search))
    - [[The Plurality Book]]の内容に対するベクトル検索を提供
    - データソースはGithub上の原稿とその機械翻訳
        - RadicalxChange Blogの記事も追加で採集
    - [/plurality-japanese/Vector Searchを実装する](https://scrapbox.io/plurality-japanese/Vector Searchを実装する)
    - 10/18 [/plurality-japanese/RxC Blogを検索対象にする](https://scrapbox.io/plurality-japanese/RxC Blogを検索対象にする)
        - Markdownからの対象追加
- 2024-03-21 [/plurality-japanese/ベクトル検索の改善](https://scrapbox.io/plurality-japanese/ベクトル検索の改善)
- 2024-04-02
    - [/plurality-japanese/⿻VecSearchJA](https://scrapbox.io/plurality-japanese/⿻VecSearchJA) リリース
    - 作業ログ: [[pVectorSearch2024-04-02]]

新機能案
- GETでURLフラグメントにScrapboxのページ名を渡す
- 検索結果から「それを積んでプロンプト実行」を可能にする
- 検索対象の切り替え機能
- 同一ページ内のヒットを除外するオプション

課題と今後
- アップデート機能の実装
- サービスの安定運用 (ログ管理、エラー対応など)
- 非公開ソースを含む検索結果の慎重な扱い
- [[熟議]]のための[[前提知識の共有]]をどう実現するか

以上が、pVectorSearchプロジェクトのこれまでの概要です。ベクトル検索技術を使って個人の知識ベースを横断的に検索し、協働や合意形成に役立てる可能性を模索するプロジェクトとして進められています。今後もアップデートと改善を重ねつつ、知的生産や議論の場に新しい選択肢を提供していく挑戦が続きそうです。


<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>簡潔にして
<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>VectorSearchの開発進捗を簡潔にまとめると以下のようになります。
- 2023年4月29日~5月31日: ベクトル検索に関する初期考察とAPI構想
- 2023年6月2日~5日: ローカル環境での実験、Scrapbox ChatGPT Connectorの知見応用
- 2023年6月6日: 管理機能実装、"西尾のベクトル検索"公開
- 2023年6月7日: 他の人のScrapboxをクロール、複数人のScrapbox横断検索実現
- 2023年6月13日~15日: 非公開資料の検索対象化と蔵書横断検索の検討
- 2023年6月27日: Omoikane Embed開発、Democratic Inputs to AIフォーラム(omoikane)に導入
- 2023年8月9日: コードの整理と他プロジェクトへの導入容易化
- 2023年10月17日: The Plurality Bookの内容に対するベクトル検索Plurality Vector Searchリリース
Omoikane Embedは、Scrapboxや他のソースのコンテンツを自動ベクトル化し、Qdrantデータベースにアップロードしてベクトル検索を提供するシステムです。2023年6月と7月にそれぞれバージョンアップを行い、機能を拡張しています。
