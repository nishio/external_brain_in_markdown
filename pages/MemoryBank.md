---
title: "MemoryBank"
---

[https://ar5iv.labs.arxiv.org/html/2305.10250](https://ar5iv.labs.arxiv.org/html/2305.10250)

<img src='https://scrapbox.io/api/pages/nishio/DR/icon' alt='DR.icon' height="19.5"/>
MemoryBank (Zhong et al., arXiv 2023): LLM向けに設計された長期記憶機構です。過去の会話全文や要約、ユーザの人物像（嗜好や人格）といった情報を「メモリーバンク」に格納し、対話中に関連記憶を検索・参照します​。特徴は[[エビングハウスの忘却曲線]]理論に基づく動的な記憶更新で、時間経過と重要度に応じて記憶の強度を増減させます​。具体的には各記憶項目に「利用頻度による強度」を持たせ、長期間参照されない記憶は強度が減衰し人間同様に忘却される一方、一度でも想起された記憶は強化され寿命が延びます​。
- これ面白いな<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
    - この外部脳でも、まずは雑にメモを取っておき、しばらく経ってからまた参照した時に、より参照されやすくするために整備をしている
    - この発想自体は海馬の振る舞いを参考にした

この仕組みによりメモリ容量を無制限に拡大せず重要な記憶を選別保持します。MemoryBankはChatGPTなど既存モデルにも外付け可能であり、実装例として長期対話ボット「SiliconFriend」に組み込まれました​。SiliconFriendは心理カウンセリング対話を模した評価で、ユーザの感情に共感しつつ過去の出来事を適切に想起でき、人と長期対話するコンパニオンAIとして有望であることが示されています​。