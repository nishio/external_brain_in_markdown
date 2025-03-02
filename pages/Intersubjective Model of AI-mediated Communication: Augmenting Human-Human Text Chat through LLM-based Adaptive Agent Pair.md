---
title: "Intersubjective Model of AI-mediated Communication: Augmenting Human-Human Text Chat through LLM-based Adaptive Agent Pair"
---


![image](https://gyazo.com/3aeba9eb57caa45165af87dccbc57406/thumb/1000)
- 青山さん([[Bluemo]])が研究している新しい形のコミュニケーション
- from [/blu3mo-public/Intersubjective Model of AI-mediated Communication: Augmenting Human-Human Text Chat through LLM-based Adaptive Agent Pair](https://scrapbox.io/blu3mo-public/Intersubjective Model of AI-mediated Communication: Augmenting Human-Human Text Chat through LLM-based Adaptive Agent Pair)
- [https://arxiv.org/abs/2502.18201](https://arxiv.org/abs/2502.18201)

<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>この論文は、各ユーザーが独自のチャット環境で会話を行う際に、LLM搭載のAIエージェントが仲介し、情報を抽出・交換することで、従来の直接的な情報伝達を超えた柔軟な対話を実現する新しいモデル「Intersubjective Model」を提案しています。

基本構造:
- 各ユーザーは個別のチャット環境におり、各環境にはAIエージェントが配置されています。エージェントはユーザーの発言から重要な情報を抽出し、相手側のエージェントに送信。受け取った情報を基にユーザーへ返答を生成します。

特徴:
- 内側フィードバック: ユーザーと自分のエージェント間で即時応答が得られ、会話のリズムを維持
- 外側フィードバック: エージェント同士が情報を交換し、会話全体の意味や意図を補完

応用例: 活発な会話、集中した議論、言語の壁や世代間ギャップの克服などに対応可能
実装例:
- シンプルなチャットUIとGPT-4oを利用したエージェント機能（抽出と会話生成）を組み合わせ、自然な対話リズムを実現するシステムを構築しています。

このモデルにより、ユーザーは各自の主観的な環境でありながら、AIを介した情報交換で豊かなコミュニケーションが可能になります。
