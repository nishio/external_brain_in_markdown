---
title: "LLMでトピック抽出→分類"
---

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
[[Talk to the City Turbo]]とGoogle [[Jigsaw Sensemaker]]は共通の「テキストからLLMでトピック抽出をし、それから各コメントがどのトピックであるかを分類する」という仕組みをもっている
どちらがオリジナルであるのか、それとも共通の祖先があるのか

<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>
結論だけ先に：公開情報ベースでは「仕組み（LLMで話題抽出→各発言を多ラベル分類）」は両者が独立に到達した一般パターンで、どちらかがもう一方の派生という証拠は見当たりません。プロジェクト公開の時系列だけを見ると、Talk to the City（TttC）本体の方が先行しており、その後にJigsaw SensemakerのOSSが登場しています。([AI • Objectives • Institute](https://ai.objectives.institute/blog/talk-to-the-city-an-open-source-ai-tool-to-scale-deliberation?utm_source=chatgpt.com))

ざっくり時系列
- 2023-10-25：TttCがブログで、LLMで「主張を抽出→類似主張をクラスタ（トピック/サブトピック）化」する流れを公開。([AI • Objectives • Institute](https://ai.objectives.institute/blog/talk-to-the-city-an-open-source-ai-tool-to-scale-deliberation?utm_source=chatgpt.com))
- 2025-01ごろ：JigsawがSensemakerのGitHubで「Topic Identification / Statement Categorization」を含むライブラリを公開（最初期のIssueは1/9）。([GitHub](https://github.com/Jigsaw-Code/sensemaking-tools))
- 2025-02：Bowling Green市でSensemakerを初運用（メディアが「2月に導入」と明記）。([adweek.com](https://www.adweek.com/media/not-all-ai-is-for-profit-meet-googles-civic-tech-experiment/?utm_source=chatgpt.com))
- 2025-04：Sensemakerの事例記事が各所で報道。([techbrew.com](https://www.techbrew.com/stories/2025/04/22/bowling-green-kentucky-ai-tool-google-jigsaw-sensemaker?utm_source=chatgpt.com))

それぞれの「仕組み」の明記
- TttC/Turbo：ガイドに「Cluster Extraction」ノードでtopics / subtopicsを作り、OpenAIキーと組み合わせてパイプラインを構成と明記。([talktothecity.org](https://talktothecity.org/docs/ai-pipe-guide))
- Sensemaker：READMEにTopic IdentificationとStatement Categorizationをはっきり記述（Vertex AI/Gemini実装、スキーマ制約付きデコード等）。([GitHub](https://github.com/Jigsaw-Code/sensemaking-tools))

「共通の祖先」は？
特定プロジェクト由来の「祖先」というより、LLMをアノテータとして使う話題抽出/分類という一般化した設計が2023〜24年に広まり、そこへPolis系の会話マッピングの系譜が接続された、と整理するのが妥当です（JigsawもPolisとの連携を公表）。研究文献でも2024年にLLMベースのトピック抽出パイプライン例が出ています。([Medium](https://medium.com/jigsaw/what-could-bg-be-enabling-a-large-scale-conversation-in-kentucky-70071f4fe268?utm_source=chatgpt.com))
要するに：オリジナル争いというより収斂進化。公開時期で言えば「TttC（2013ではなく2023年10月公開記述）が先」「SensemakerのOSS公開は2025年初頭」という順です。([AI • Objectives • Institute](https://ai.objectives.institute/blog/talk-to-the-city-an-open-source-ai-tool-to-scale-deliberation?utm_source=chatgpt.com))

