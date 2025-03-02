---
title: "Aggressive behaviour of anti-vaxxers and their toxic replies in English and Japanese"
---

Aggressive behaviour of anti-vaxxers and their toxic replies in English and Japanese | Humanities and Social Sciences Communications
[https://www.nature.com/articles/s41599-022-01245-x](https://www.nature.com/articles/s41599-022-01245-x)
<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>
この論文は英語と日本語のツイッターデータを分析し、反ワクチン派（アンチワクチン派）のリプライ行動の特徴を明らかにしました。主な発見は以下の通りです。
- 反ワクチン派は、他の信念を持つユーザー、特に中立的なアカウントに対して最も積極的にリプライを送っており、その内容は有意に毒性が高く否定的です。これらのリプライはワクチン関連の投稿に向けられることが多いです。
- フォロワー数が多い影響力のあるユーザーやアカウント（医療関係者、科学者、政策立案者、メディア関係者など）は、反ワクチン派から最も毒性の高いリプライを受ける傾向にあります。
- 英語では少数のフォロワーしかいないプロワクチン派アカウントも高い毒性のリプライを受けていますが、日本語ではそのような傾向は見られませんでした。

これらの結果は、反ワクチン派の攻撃的な行動に対抗するための言語に依存した、そして言語に依存しない対策への洞察を提供しています。プラットフォームは反ワクチン派の言説を他のユーザーに露出させないための措置を取り、プロワクチン派は反ワクチン派からの毒性の高い感情的なリプライに備えるべきだと提言しています。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>具体的な手法は？

<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>本研究では以下のような具体的な手法が用いられました。
- データ収集: 2020年2月から12月までのCOVID-19関連のツイートを継続的に収集。ワクチン関連のキーワードを含むツイートを抽出。
- RTネットワークに基づくクラスタリング: ユーザーをワクチンに対するスタンス（反ワクチン派、中立派など）に分類するため、RTネットワーク上でコミュニティ検出を行いました。
- リプライ行動の分析: 反ワクチン派のリプライ頻度、対象クラスタ、リプライ先の人気度などを調査。
- 毒性の測定: Google の[[Perspective API]]を用いてリプライの攻撃性を測定。日本語ツイートは翻訳後に毒性を測定。
- 感情分析: 感情辞書（LIWC 2015、Warrinerらの辞書）を用いて、リプライのネガティブ・ポジティブ度合い、感情の覚醒度を測定。
- フォロワー数と毒性の関係性の分析: リプライ先ユーザーのフォロワー数と、受け取ったリプライの最大毒性値の相関を調査。

これらの手法を駆使することで、英語・日本語という異なる言語圏において、反ワクチン派の攻撃的リプライ行動の特徴を多角的に分析しました。