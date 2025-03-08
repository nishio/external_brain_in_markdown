---
title: "10 Years of Git: An Interview with Git Creator Linus Torvalds"
---

[10 Years of Git: An Interview with Git Creator Linus Torvalds - Linux Foundation](https://www.linuxfoundation.org/blog/blog/10-years-of-git-an-interview-with-git-creator-linus-torvalds)(2015)
[本の虫: gitの10周年を記念したLinus Torvalsへのインタビューの翻訳](https://cpplover.blogspot.com/2015/04/git10linus-torvals.html)
<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>
## 1. 記事全体の解説
この記事は、[[Git]]の生みの親である[[Linus Torvalds]]([[リーナス・トーバルズ]])氏へのインタビュー形式で、Gitが誕生した背景やその設計思想、現状での運用について語られています。
- 背景: 当時、Linuxカーネル開発では[[BitKeeper]]というプロプライエタリなツールを使用していましたが、その制約（特に変更権限の管理に関する政治的な問題）に不満があったため、トーバルズ氏は自ら新たな分散型ソース管理システム（Git）を作り上げました。
- 開発経緯: Gitは短期間で基本機能が実装され、特に「[[自分自身のリポジトリを持つ]]」という分散の考え方が、従来の中央集権的なシステムの問題を解消するために重要でした。
- 評価: トーバルズ氏は、GitがLinuxカーネル開発に非常に適していると評価しており、その柔軟性と効率性が他のプロジェクトでも広く採用される要因になったと述べています。

## 2. 「分散」に関する記述の引用と解説
トーバルズ氏は、分散型ソース管理の最大の利点について以下のように述べています。

>  "The big thing about distributed source control is that it makes one of the main issues with SCM’s go away – the politics around 'who can make changes.'"
>  （分散型ソース管理システムの大きな特徴は、SCMが抱える主要な問題の一つ、つまり「誰が変更できるか」という権限を巡る政治的な問題を解消できる点にある。）

### 解説
:
この引用からわかるのは、従来の集中管理型のシステムでは、誰がコードに変更を加えられるかという管理のための政治的なやりとりが発生しやすかったという点です。Gitでは、各開発者が自分自身のリポジトリを持つことで、中央の承認プロセスに頼らずに自由に作業できるため、このような「権限を巡る政治的問題」が大幅に軽減されます。結果として、よりスムーズで柔軟な開発フローが実現し、多くのプロジェクトがGitを採用する大きな理由となりました。

---
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
- 結局[[中央集権の利便性]]が勝って[[GitHub]]を使う人が大半になってしまったように思う
- 僕が学生だった頃だと研究室マシンに寮からSSH可能にして[[ベアリポジトリ]]を置いたりとかしてたんだけどね
