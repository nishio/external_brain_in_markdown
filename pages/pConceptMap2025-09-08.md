---
title: "pConceptMap2025-09-08"
---

from [[A Framework for Constructing Concept Maps from E-Books Using Large Language Models: Challenges and Future Directions]]
[[pConceptMap]]2025-09-08
- [[Concept Map]]

memo
[https://chatgpt.com/c/68ba96f1-2650-8320-84a6-33bb3f7838ae](https://chatgpt.com/c/68ba96f1-2650-8320-84a6-33bb3f7838ae)

> 4段階：①セクション分割→②概念抽出→③関係同定→④統合
- 抽出された概念のラベル
- その間の関係の同定
- この流れは[[Keichobot]]にも関係しそうだ<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>

---
実験結果まとめ：
📊 生成された概念（5個）：
- globalization (グローバル化) - core
- digital technology (デジタル技術) - core
- democracy (民主主義) - core
- plurality (多元性) - core
- collaboration (協働) - supplementary

🔗 概念間の関係（4つ）：
- globalization → digital_technology (prerequisite_of, 0.90)
- democracy ← collaboration (part_of, 0.85)
- digital_technology → plurality (example_of, 0.80)
- democracy ↔ globalization (contrasts_with, 0.75)

---
おおよその流れは理解できた。
- まず与えられたドキュメントから「重要そうなキーワード」を抽出し、
- それからそのキーワードリストとドキュメントのセットを与えて「関係性」を抽出する


費用検討
- いまgpt-4o-mini
- > 開発者向けの料金は、100万入力トークンあたり15セント、100万出力トークンあたり60セント（標準的な書籍の約2500ページに相当）です。...ChatGPT では、本日より Free、Plus、Team ユーザーが GPT‑3.5 を置き換え GPT‑4o mini にアクセスできるようになります。
    - [https://openai.com/ja-JP/index/gpt-4o-mini-advancing-cost-efficient-intelligence/](https://openai.com/ja-JP/index/gpt-4o-mini-advancing-cost-efficient-intelligence/)
- [https://openai.com/ja-JP/api/pricing/](https://openai.com/ja-JP/api/pricing/)
    - GPT-5, mini, nano
        - 出力で $10, $2, $0.4

GPT-5-mini vs 他モデル比較
🏆 GPT-5-mini の特徴
📊 概念の詳細度:
- より詳細で正確な概念定義
- **⿻（ユニコード記号）**という細かい要素まで抽出
- 日本語と記号を組み合わせた複合的な理解
🔗 関係性の精度:
- 6つの関係性を抽出（他モデルは4つ程度）
- 高い信頼度（0.90-0.95）
- 相互関係も捉えている（uses ↔ example_of）

![image](https://gyazo.com/851cbee2aebdb5d10fc28abccbdef89a/thumb/1000)
双方向の矢印が重なるのは見づらいので合成したいね
- そもそもpart_ofみたいな関係性を抽出しているのはLLM以前の思想、関係も言葉で説明させればいい
- [[関係をシンボル化しない]]

[[テキストに根差した関係抽出]]
- [[関係は意味であり逆もまた真]]

next [[pConceptMap2025-09-09]]
