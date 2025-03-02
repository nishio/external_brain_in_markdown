---
title: "2023年SlackのUI設計変更"
---

[Slackの“個人ミュート”機能が話題　「これが必要な職場はヤバい」「ハラスメント対策になる」など賛否両論 - ITmedia NEWS](https://www.itmedia.co.jp/news/articles/2309/08/news131.html)
- > 企業向けコラボレーションツール「Slack」の新機能「Hide Person」が、9月6日ごろから話題になり始めている。これは特定のメンバーのメッセージを非表示にしたり通知させないようにしたりする機能


> [ssig33](https://twitter.com/ssig33/status/1698608372625678416) 新しいSlackのUIって最大の変更点がDMが第一級市民に格上げされる点で、これってつまり Slack 導入企業における従業員たちのSlackの主な使い方ってDMで個人間で秘密の会話をするというものなんでしょうね。それは現実そうなのかもしれないけど、コラボレーションを後退させる決断をしたと思う。
- > [ssig33](https://twitter.com/ssig33/status/1698608374169182667) Slackは現実的にDMプラットフォームとして使われているからDMを使いやすくしよう！！！というのはプロダクトのコンセプトの敗戦受け入れであって、プロダクトにも導入顧客にもあまりポジティブな影響を与えないのではないか?と思っています。
> [nishio](https://twitter.com/nishio/status/1698713218196361252) 3から4にどうやって移行するか悩んでたのにSlackは3から2に移行するのか…
- > [nishio](https://twitter.com/nishio/status/1698713355522081066) これの話: [[メッセージ伝達の進化]]

> [sora_h](https://twitter.com/sora_h/status/1701831750345957676) Slack、public channel の利用具合を stats に表示する程度にはその重要性を認識してるんだろうなと思ってたのに DM を是とし始めたのは本当に最悪だし Salesforce に染まった結果なんだろうかという邪推をしてしまう



ごたつきのメモ

> [akiroom](https://twitter.com/akiroom/status/1702168295795777576/photo/1) Slackの新しいUI、届いたメンションを一覧で見ようとすると全ての本文が「…」で省略されて読めない。これが本番環境に出てくる開発体制が大変興味深い。 [https://gyazo.com/cee253b7bdaf33d190cde0be5c72a53a…](https://gyazo.com/cee253b7bdaf33d190cde0be5c72a53a…)
>  ![image](https://pbs.twimg.com/media/F59RCy8XIAAS8xH?format=jpg&name=large#.png)
- > [akiroom](https://twitter.com/akiroom/status/1702168463220113678) 自分で使ってたら絶対こうはならないと思うんだけど、なんでこのUIにしたんだろう。
- > [akiroom](https://twitter.com/akiroom/status/1702168745698037947) 逆にドッグフーディングしながら開発しているため、Slackを画面共有した結果、プライベートチャンネルやDMのメンションが表示されてしまい、隠すようになったとか…？
- > [akiroom](https://twitter.com/akiroom/status/1702168295795777576/photo/1) 「開発体制が大変興味深い」は婉曲表現で、実際のところ頭は沸騰していてFワード連呼してるのをグッと押さえています。


> [9d](https://twitter.com/9d/status/1702207259970064494/photo/1) Slack、インターフェイス変わってから、この状態で他のワークスペースのアイコンが見えないし、メンションついてるかも分からなくて扱いにくい。設定で前の状態に戻せるのかな。
>  ![image](https://pbs.twimg.com/media/F590ZJObcAAOFPW?format=png&name=small#.png)


