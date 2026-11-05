---
title: "AI Swarm"
---

2023 初期の研究
- CAMEL・AutoGenなどのLLMマルチエージェント
    - 異なる役割を与えたLLMエージェントが対話しながら共同作業する研究・実装を公開。初期の代表例。
    - 自然言語で相談・批評・分業するエージェント群が実装される。群れの構成要素自体が、高度な言語処理能力を持つようになった。
    - 2023/3/31	[[CAMEL]]
        - 異なる役割を与えたLLMエージェントが対話しながら共同作業する研究・実装を公開。初期の代表例。
        - [2303.17760 CAMEL: Communicative Agents for "Mind" Exploration of Large Language Model Society](https://arxiv.org/abs/2303.17760)
    - 2023/9/25	[[AutoGen]]
        - Microsoft Researchの開発基盤。複数エージェントの自動チャットと、「受信時にどう応答するか」を構成できた。一般利用製品への内蔵とは別。
        - [AutoGen: Enabling next-generation large language model applications - Microsoft Research](https://www.microsoft.com/en-us/research/blog/autogen-enabling-next-generation-large-language-model-applications/?utm_source=chatgpt.com)


2024~2025 エージェント間のコミュニケーション方法が徐々に整う
- 2024年10月	OpenAI Swarm
    - エージェント間の処理の引き継ぎ〔handoff〕を示す実験的ライブラリ。公式Cookbookは10/10付。
- 2025/3/11：OpenAI Agents
    - SDK公開。 エージェント間の処理の引き継ぎ〔handoff〕を公式SDKで提供
- 2025/4/9：GoogleがA2Aを発表。 異なるベンダー・フレームワークのエージェントが通信するための公開プロトコル
- 2025/6	Claude Flow〔現Ruflo〕
    - Claude Code向けの外付け統括基盤。6/10に初公開、6/11に初期swarm機構。通信単体より、複数エージェントの調整全体を扱う。
- 2025/7	Claude Code：カスタムsubagents
    - v1.0.60で専門の子エージェントを定義可能に。これはまず委任機能の節目。
- 2025/10〜12	MCP Agent Mail
    - エージェントの名前、受信箱、返信、検索可能な会話スレッド、ファイルの使用予約。10/23から開発履歴があり、最初のGitHub Releaseは12/31。GitHub

2026年初頭
- 2026/1/1	Gas Town
    - 複数のコーディングエージェントを、メール、作業割り当て、tmux経由の通知で協働させる環境を公開。
- 2026/1	pi-messenger
    - pi向け拡張。エージェント発見、直接メッセージ、全体への通知、ファイル予約。CHANGELOGでは1/20が初版。
- 2026/1〜2	Codex：実験的マルチエージェント
    - 1月には実験版の利用が確認でき、2月のv0.102.0で役割を設定する機能が追加された。段階導入なので、単一の開始日にはしにくい。
- 2026/1/22	Cursor 2.4：Subagents
    - 独立したコンテキストを持つ子エージェントへの並列委任を製品機能として導入。
- 2026/2/5	Claude Code：Agent Teams
    - 研究プレビュー。チームメンバー同士が直接メッセージを交換し、共有タスクを調整する機能。
- 2026年初頭〜春	Gemini CLI：リモートエージェント連携
    - A2Aを使って外部エージェントへ委任。少なくとも3/11のリリースでは認証機能の拡充を確認できる。通常のsubagentsについては4/15に公式紹介。

エージェント間の直接コミュニケーション
- 2026/8/7	Claude Code：[[Cross-session messaging]]
    - v2.1.224で、別々に起動したセッションを発見する`ListAgents`と、通信する`SendMessage`を導入。最初はmacOS・Linux、Windowsは後続版で対応。
    - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> 最初に見た時はびっくりした
        - 知らない人のために簡単に説明すると同一プロジェクトフォルダ内で複数のClaude Codeを動かしてるとそれらが互いに話し合って調整をするようになっている

個人的には[[agmsg]]が印象的だった(2026-05-27)
- [[複数AIエージェントに共通のDBを読ませる]]というページにメモしていた
最近(2026-10-16)だとKenn Ejimaさんが["/relay"](https://x.com/kenn/status/2110778316752089584?a=9Gc9v5EuiuQ8tJYnCvM&s=20)なるものを作って盛んに投稿してる
これらは要するに異なるエージェント間で情報共有したいというニーズから生まれてきている

初期の群知能研究
1959年	Grasséが[[スティグマジー]]を提唱
- シロアリの巣作りなどで、環境に残された作業の痕跡が次の個体の行動を導く。直接会話しなくても協調が成立する仕組み。
- [A brief history of stigmergy - PubMed](https://pubmed.ncbi.nlm.nih.gov/10633572/)
1986年開発・1987年発表	Reynoldsの[[Boids]]
- 「衝突を避ける・近隣と向きを合わせる・集まる」という局所的なルールで、鳥の群れのような動きを生成。全体の動きを指示する司令塔を置かない設計。
1989年	BeniとWangがswarm intelligenceという用語を導入
- ロボット群の集団的な知能を研究対象として言語化。
1990年代	蟻コロニー最適化・粒子群最適化
- 群れの振る舞いを、経路探索や数値最適化のアルゴリズムへ。DorigoのAnt Systemは1992年の博士論文、KennedyとEberhartのPSOは1995年。
