---
title: "Long-term Dialogue Agent"
---

Hello Again! LLM-powered Personalized Agent for Long-term Dialogue
[https://arxiv.org/abs/2406.05925#:~:text=the%20Long,Agent%20are](https://arxiv.org/abs/2406.05925#:~:text=the%20Long,Agent%20are)
![image](https://gyazo.com/9ae1d031a99e3fb473113497f9842c29/thumb/1000)

<img src='https://scrapbox.io/api/pages/nishio/DR/icon' alt='DR.icon' height="19.5"/>
[[LD-Agent]] (Li et al., NAACL 2025): Long-term Dialogue Agent と銘打ったモデル非依存のフレームワークで、対話の出来事（イベント）記憶と人格情報を分離管理する点が特徴です​。構成は(1)過去セッション全体を蓄積する長期メモリと、現在セッションの短期メモリ、(2)ユーザおよびエージェント自身の動的な人格モデル, (3)応答生成モジュールからなります​。各セッション終了後、重要な出来事を要約エントリとして長期メモリに保存し、新たなユーザ情報は人格プロファイルに更新します。また検索時にはトピックベースのメモリ検索を導入し、話題に沿った過去エピソードを効果的に抽出します​。例えば趣味に関する対話では趣味カテゴリの記憶に絞って検索することでノイズを減らしています。抽出された過去メモリと人格情報を入力に加えて応答を生成することで、ユーザとエージェント双方のキャラクターに沿った発話が可能となります​。LD-Agentはモデルサイズや対話ドメインに依存せず適用でき、実験ではPersonaChat派生のマルチセッション対話など複数データセット上で汎用性と効果が示されています​。