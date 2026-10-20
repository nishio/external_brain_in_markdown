---
title: "Civic AI"
---

Civic AI — [[6-Pack of Care]]
- > A governance framework by Audrey Tang and Dr Caroline Emmer De Albuquerque Green that translates Joan Tronto's care ethics into six machine-codeable design primitives for Civic AI — bounded, place-specific AI stewards engineered for relational health, not unbounded optimisation.
- [https://github.com/audreyt/civic.ai](https://github.com/audreyt/civic.ai)
    - [Civic AI — 6-Pack of Care](https://civic.ai/)の文章はここにある

<img src='https://scrapbox.io/api/pages/nishio/Claude/icon' alt='Claude.icon' height="19.5"/>
Competence の変化
二段階で起きています
1. 2026-02-18（commit 587b914）
- コミットメッセージは「move RLCF to Pack 4, add security to Pack 3」です。
- RLCF（[[コミュニティのフィードバックによる強化学習]]）は [[care-giving]] ではなく [[care-receiving]] に属する、という理由で Competence から Responsiveness へ移されました。[[trust-under-loss]] もこのとき RLCF と一緒に移っています。
- 空いた Competence に[[セキュリティ]]の段落が入り、Rule of thumb は「Security failures are moral failures.」になりました。言い切りの短い形です。

2. その後の言い回しの調整
:
| 日付 | Rule of thumb |
| -- | -- |
| 02-18 | Security failures are moral failures. |
| 02-21（a559c4c） | …are moral failures of those who build and deploy, not merely technical oversights. |
| 06-30（979d560） | …reveal moral failure in build and deployment before they read as technical oversights. |
「倫理の失敗である」から「倫理の失敗を露わにする」へ、少しずつ柔らかくなっています。
段落本文の例示も変わりました。最初の版は「scope creep」で、6/12 に「lateral movement」になっています。

流れとしての読み：マニフェストの初版は 2025-09 で、セキュリティを入れたのは約5か月後です。Audrey は 2025-09 の時点では、セキュリティを 6-Pack の中心に置いていなかったことになります。この後から加わった部分に触れる問いです。「なぜセキュリティを後から Competence に入れたのか」は、Audrey に聞ける自然なとっかかりになります。


Kami の変化
こちらも二段階です
1. 2026-02-21（a559c4c）
- コミットメッセージは「strengthen philosophical foundations with Tronto-grounded repairs」です。
- 「[[boundedness is not intrinsic but engineered]]」と「[[imperial creep]]」がマニフェスト本文に入りました。
- コミットメッセージは「Clarify kami boundedness as engineered constraint, not natural property」です。
- 同じコミットで、他にも直しています。
    - [[is-ought問題]]を「解く」とは言わず、Tronto の「in the middle of things」から始める形に改めた
    - 台湾の信頼回復を「bridging アルゴリズムのおかげ」とする因果の言い過ぎを、「not alone, but as part of a broader democratic renewal」に弱めた
    - 政策は horizontal だけでなく「also」horizontal にも目を向けよ、に直した
- 全体として、批判に耐えるよう主張を締め直した回に見えます。

2. 2026-03-17（6e8e74f）
コミットメッセージは「clarify Kami as bounded relational steward」で、本文に理由が書かれています。
- > Per Anne-Marie Slaughter's feedback, add paragraph distinguishing a local Kami from both an [[omniscient Singleton]] and a [[closed-community voice]], and making explicit that overlapping memberships prevent any single Kami from dominating the whole person.
- 「[[閉じた共同体の声ではない]]」の段落は、[[Anne-Marie Slaughter]] の指摘を受けて足されたものです。Kami が排他的な共同体の代弁者と読まれうる、という批判への応答です。

ついでに分かったこと
- ほぼ全部のコミットが Audrey 本人によるもので、多くに Claude が Co-Author として付いています（Opus 4.6 や Sonnet 4.6）。Audrey は AI と一緒にマニフェストを書き直し続けています。これ自体が話題になり得ます。
- Civic AI の本が進行中のようです。2026-09 以降、マニフェストを本に合わせる変更が続いています：「Carry the Wiley copyedit fact-checks」（9/26）、「align bilingual site with the Civic AI book」（9/29）、「carry the book's final corrections to the site」（10/2）。サイトの FAQ には「Book Chapters 3-8 correspond to site Packs 1-6」とあります。書名や刊行時期はまだ確かめていません。インタビューの時期によっては、本が出た直後かもしれません。
