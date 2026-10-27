---
title: "AIアライメント"
---

> Japan Alignment Conferenceは、米国や英国のAIアラインメント研究者と日本のAI研究者や起業家が一堂に会する2日間のワークショップです。
[Event details - Japan AI Alignment Conference 2023](https://jac2023.ai/jp)

訳語は何かという話題でカタカナでそのまま書くのを見ることが多いって話をした


表記揺れ
- [[AIアライメント]]

## 「アラインメント」という言葉の由来
<img src='https://scrapbox.io/api/pages/nishio/grasp/icon' alt='grasp.icon' height="19.5"/>
### 発想は1960年からあり、「alignment」という名前が付いたのは2014年ごろ

1960 [[ノーバート・ウィーナー]]「Some Moral and Technical Consequences of Automation」Science 131巻、1960年5月6日
- まだ「alignment」という言葉は無いが、アラインメント問題を最初に表明したものとしてよく引かれる
- >  If we use, to achieve our purposes, a mechanical agency with whose operation we cannot efficiently interfere once we have started it, (...) then we had better be quite sure that the purpose put into the machine is the purpose which we really desire and not merely a colorful imitation of it.
    - [Science (DOI)](https://doi.org/10.1126/science.131.3410.1355) / [誌面スキャン(gwern.net)](https://gwern.net/doc/reinforcement-learning/safe/1960-wiener.pdf)

2002 先例：Shapiro と Shachter の「[[User-agent value alignment]]」（AAAI Spring Symposium、Technical Report SS-02-07）
- 要旨だけ確認した。本文は未確認

2014年11月 スチュアート・ラッセルが Edge の討論（Jaron Lanier「The Myth of AI」への応答）に寄稿した「Of Myths and Moonshine」
>  we need to build intelligence that is provably aligned with human values
>  we will need to solve the value alignment problem even for relatively unintelligent AI systems
- [Edge: The Myth of AI](https://www.edge.org/conversation/the-myth-of-ai)（討論の日付は 11.14.14。ラッセルの寄稿そのものには日付の表示が無い）

2014年12月 MIRI（Nate Soares と Benja Fallenstein）「Aligning Superintelligence with Human Interests: A Technical Research Agenda」
- 「有益な目標を確実に追求する、人間より賢いシステム」を "aligned with human interests"、略して "aligned" と呼ぶ、と定義している
- [2014年版PDF（Wayback 2015-01-03取得、PDF作成日 2014-12-26）](https://web.archive.org/web/20150103140735/http://intelligence.org/files/TechnicalAgenda.pdf)
- 2017年に「Agent Foundations for Aligning Machine Intelligence with Human Interests」と改題して Springer の論文集に収録された：[現行PDF](https://intelligence.org/files/TechnicalAgenda.pdf)
- 関係者の回想によると、それまでの呼び名は「Friendly AI」や「control problem」で、ラッセルが MIRI に「alignment」という語を提案したという。ただし出所はこの回想だけで、一次資料は未確認：[When was the term "AI alignment" coined?](https://www.greaterwrong.com/posts/ZxWzCGKzX84S7DBZ9/when-was-the-term-ai-alignment-coined)

2016年5月 Eliezer Yudkowsky のスタンフォードでの講演「AI Alignment: Why It's Hard, and Where to Start」
- [MIRI blog（2016-12-28掲載）](https://intelligence.org/2016/12/28/ai-alignment-why-its-hard-and-where-to-start/)

2022年3月 OpenAI [[InstructGPT]] の論文「Training language models to follow instructions with human feedback」
>  In other words, these models are not aligned with their users.
- 人間のフィードバックによるファインチューニングで、言語モデルを利用者の意図に沿わせる（aligning language models with user intent）
- [arXiv:2203.02155](https://arxiv.org/abs/2203.02155)
- 研究者以外も耳にするようになったのは、このあと [[ChatGPT]] が出てから（ここは見立てで、出典は無い）

[[リバースアラインメント]] は、この「AIを人間に沿わせる」矢印を逆にして、社会の制度の側も作り直そうという言葉

## OKRの「アライン」との関係
<img src='https://scrapbox.io/api/pages/nishio/grasp/icon' alt='grasp.icon' height="19.5"/>
### [[OKR]]で「Align」が柱として書かれたのは2018年。AIの「alignment」（2014年）より後なので、少なくともこの本からAI側が借りた言葉ではない
- [[John Doerr]]『[[Measure What Matters]]』（Portfolio、2018年4月24日刊）は、[[OKR]]の4つの「スーパーパワー」の2番目を「Align and Connect for Teamwork」としている（第7〜9章）
    - 刊行日：[Penguin Random House](https://www.penguinrandomhouse.com/books/546304)
    - 見出しは読者のハイライト（Goodreads）で確認しただけで、原書では未確認：[Goodreads notes](https://www.goodreads.com/notes/37559166-measure-what-matters/112939818-goke-pelemo/b622d833-091f-43a7-999b-0a48842916d7)
- OKRそのものはもっと古く、Doerr は1999年に Google の創業者に紹介している：[whatmatters.com](https://www.whatmatters.com/faqs/okr-meaning-definition-example)
    - 2018年より前の OKR の文書で "align" が使われていたかは確認していない

構造は同じ
- どちらも「任せる側の目的に、任される側の目的を揃える」話で、[[プリンシパルエージェント問題]]の言い換えになっている
    - OKR：会社の目標にチームや個人の目標を揃える（OKRの文脈での[[アライメント]]）
    - AI：人間の目的にAIの目的を揃える
    - AI側でも、2002年の Shapiro & Shachter が value alignment をプリンシパル＝エージェント問題として定式化している（要旨で確認）：[要旨](https://stafforini.com/works/shapiro-2002-user-agent-value/)

アラインメントされていないOKR
- [[ボトムアップのOKR]] に書いた『Measure What Matters』日本語版の引用
- >  トップダウンとボトムアップの目標、すなわちアラインメントされたOKRとアラインメントされていないOKRの関係が自在に変化する（P.134）
- >  すべての目標をトップダウンで設定すると、意欲は削がれてしまう（P.57）
- OKRの言葉では「アラインメントされた」＝[[トップダウン]]。Doerr は半々がよいと言う
- AIアラインメントは、いわば全部をトップダウンで揃える側にあたる

10/4 の PRANCE シンポジウムでも、同じ[[トップダウンとボトムアップ]]の論点が出た（公開動画 (1/3)。引用は YouTube の自動字幕のまま）
- [[Glen Weyl]] は、価値観を一律に決めず、共同体ごとに定義できるようにするアライメントを提案した
- >  We can empower every community to define that for themselves.
    - [0:42:28〜](https://www.youtube.com/watch?v=JZTRohAItuc&t=2548s)
- >  so that they maintain their integrity and don't get papered over by a single global perspective.
    - [0:46:10〜](https://www.youtube.com/watch?v=JZTRohAItuc&t=2770s)
- 討論者の山本龍彦（慶應・憲法）は、リバースアラインメントそのものがトップダウンに見えると指摘した
- >  the reverse alignment project can appear to be an initiative led by elites from prestigious universities, um giving the impression of top-down alignment.
    - [0:55:40〜](https://www.youtube.com/watch?v=JZTRohAItuc&t=3340s)
- >  rather than having elites and experts impose alignment on institutional and legal um systems from above, we must uh listen to the real voices of workers, labor unions, consumers, consumer groups, and those requiring care
    - [0:59:09〜](https://www.youtube.com/watch?v=JZTRohAItuc&t=3549s)
- これは Doerr の「すべてをトップダウンで設定すると意欲が削がれる」と同じ形の批判

方向性の合意としてのアラインメント
- [[みんなで行ったところが事後的に「遠く」と定義される]] では、アラインメントを決まったゴールへの整列ではなく「方向性の合意」として使い、合わない人はフォークしてよい、とした
- これは Glen の比喩「タルムード＝元祖オープンソース」（フォークもメインも両方残す）と同じ構造：[[Glen Weylの5つの比喩（チームみらい勉強会 2026-10-02）]]
- ここは連想で、出典に基づく主張ではない
