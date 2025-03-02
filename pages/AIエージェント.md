---
title: "AIエージェント"
---

Googleの出しているWhite Paper(2024-09)
[Agents | Kaggle](https://www.kaggle.com/whitepaper-agents)
- [https://drive.google.com/file/d/1oEjiRCTbd54aSdB_eEe3UShxLBWK9xkt/view](https://drive.google.com/file/d/1oEjiRCTbd54aSdB_eEe3UShxLBWK9xkt/view)
<img src='https://scrapbox.io/api/pages/nishio/o1 Pro/icon' alt='o1 Pro.icon' height="19.5"/>
1. エージェントの概要
    - エージェントとは何か
        - 単独の大規模言語モデル（LLM）では得られない、外部ツールや外部データとのやりとりを可能にする仕組み。
        - ユーザーのゴールを達成するために、モデルが自律的に情報を取り込み、計画（推論）し、ツールなどを使って行動（API コールなど）できるようになる。
    - エージェントとモデルの違い
        - 単なるモデル：学習データ内の知識に基づき、ユーザーの問いに一度だけ推論し、回答する。外部のAPIやデータには標準ではアクセスしない。
        - エージェント：外部データへのアクセスや外部ツールの活用が可能で、複数ターン（マルチターン）の文脈管理や実行計画を持って問題解決を行う。
2. エージェントのコア構成（認知アーキテクチャ）
    - エージェントには大きく3つの要素があると解説しています。
        - モデル（language model）
            - 推論の中核を担う言語モデル(LLM)。ReAct、Chain-of-Thought、Tree-of-Thoughtsなどの推論フレームワークを用いて「どのツールをどう使うか」や「ユーザーの質問への回答」を考える。
        - ツール（Tools）
            - モデル単体では行えない外部システムへのアクセスやAPIコールを担う。
            - たとえば「天気情報API」「データベース更新API」「Google Flights API」「Google Search API」など。
            - [[ツール操作]]
        - [[オーケストレーション層]]（The orchestration layer）
            - モデルの出力やツールからの結果を受け取りつつ、最終的にどの順番で何を実行し、どう返答するかを制御する仕組み。
            - ここで「思考→行動→観察」というループを何度も回しながら、ユーザーのゴール達成を図る。
3. 具体的な推論・実装の流れ
    - [[ReAct]], [[Chain of Thought]], [[Tree-of-Thoughts]]
        - エージェントが「思考」を文章化する手法（思考過程を明示して推論する）や、解答に至る中間ステップをより強化する手法が紹介されている。
        - ReAct フレームワークの例では、「Thought（考え）→ Action（ツール実行）→ Observation（結果確認）」を繰り返し、最終回答を生成する流れを詳細に解説している。
    - 外部ツールを扱うための方法
        - Extensions
            - [[Vertex AI]] が提供する仕組みで、エージェントが外部APIを直接コールしてやりとりするための標準化されたインターフェース。
            - APIの引数（パラメータ）や使用例をエージェントに教えることで、エージェントが自発的に最適なAPIコールを判断して実行できる。
        - Functions（[[Function Calling]]）
            - エージェント側では「呼び出すべき関数名と引数」のみを提案し、実際のAPIコールはアプリケーション（クライアント）側で行う設計。
            - 認証やセキュリティ、バッチ実行、フロントエンドが先に介在するような場合に便利。
            - 例として「display_cities」という関数をエージェントが呼び出し、パラメータをJSON形式で返す。その後、クライアント側がAPIコールや追加処理を行うフローが解説されている。
        - Data Stores
            - RAG（Retrieval Augmented Generation）的な設計で、ベクターデータベースを活用し、ユーザーのクエリに合わせて必要な外部ドキュメントを検索・参照できる。
            - モデルの学習データにない最新情報やドキュメントを取り込み、回答の正確性・鮮度を高める。



[Building effective agents \ Anthropic](https://www.anthropic.com/research/building-effective-agents)

[AIエージェントの評価｜Weights & Biases Japan](https://note.com/wandb_jp/n/nf563ea9d3096?sub_rt=share_pb)

[The Shift from Models to Compound AI Systems – The Berkeley Artificial Intelligence Research Blog](https://bair.berkeley.edu/blog/2024/02/18/compound-ai-systems/)
