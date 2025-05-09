---
title: "Slackのシングルチャンネルゲスト難しすぎ"
---

from [[日記2022-11-22]]
Slackのシングルチャンネルゲスト難しすぎ

[[Slackのシングルチャンネルゲスト]]に招待される側
「どこから働きますか？」的なことを聞かれて「あー、ゲストチャンネルをどのワークスペースに置くかということか」と適当に個人のワークスペースを選んだが、失敗だった。
> チャンネルで連携するには、双方のオーガナイゼーションが Slack の有料プランを利用している必要があります。
[https://slack.com/intl/ja-jp/help/articles/115004151203-Slack-コネクトガイド---社外パートナーとの連携](https://slack.com/intl/ja-jp/help/articles/115004151203-Slack-コネクトガイド---社外パートナーとの連携)

> チームは現在無料トライアル中です。
>  Slack を使うのが初めての場合、まずチームは 2月18日までの 90 日間、プロプランの無料トライアルを利用できます。トライアルの終了後もこのプランを継続する場合、いつでもアップグレードできます。
> ...2月19日を過ぎると自動で Slack の無料バージョンに戻ります。
この説明を見ると、ここからプロプランの無料トライアルを開始できて、2/19まで使えそうに見える。だけどボタンを押すとクレジットカード情報の入力を要求される。

うーん、全然わからない
解釈1
- 「無料トライアル」と「無料バージョン」が同一の概念Aで「プロプランの無料トライアル」とは別の概念B
    - 今はAの状態で、何らかの理由でBに移行できない
        - 過去に一度Bをしたことがあるとか…
        - 「ワークスペースごとに1回トライアルできます」と書いてあるのけどな…
解釈2
- 「無料トライアル」が「プロプランの無料トライアル」の略で同一概念A、「無料バージョン」は別の概念B
    - すでにトライアルAが始まっていて、ボタン押した時に遷移するのは「いつでもアップグレードできる」のアップグレードをするための画面
    - 始まっているので開始のための画面が見つからないのは自然
    - 始まってるのにゲストチャンネルが見つからないのは不自然
解釈3
- 3つ全部異なる概念で、僕がプロプランのトライアル開始ページを見つけられてないだけ

(1) Slackbotからのメッセージ
> @nishioさんが外部オーガナイゼーションXとの共有チャンネルYに加わりました＊。
>  Shared共有チャンネルは Slack の有料プランで使える機能です。あなたのチームでは、プロプランの無料トライアルを通してこの機能を90日間お試しいただけます。クレジットカードは不要です。
これについてるリンクをクリックすると(2)に飛ぶ

(2)[Slack コネクトガイド : 社外パートナーとの連携 | Slack](https://slack.com/intl/ja-jp/help/articles/115004151203-Slack-コネクトガイド---社外パートナーとの連携)
この記事にこう書いている
> チャンネルで連携するには、双方のオーガナイゼーションが Slack の有料プランを利用している必要があります。
> Tip : Slack をまだ使用していないパートナーやフリープランを使用しているパートナーがいる場合は、Slack コネクトを無料で試してみるよう招待できます。
"Slack コネクトを無料で試してみるよう招待"は(3)につながっている

(3) [Slack コネクトをパートナーに紹介する方法 | Slack](https://slack.com/intl/ja-jp/resources/using-slack/introducing-your-partners-to-slack-connect)
> パートナーが有料の Slack プランに登録していない？ご心配なく！
>  パートナーが Slack の無料バージョンを利用していたり、Slack をまったく使っていなかったりする場合もあるでしょう。Enterprise Grid プランを利用している場合、フリープランのチームが、アップグレードや無料トライアルの必要なく、招待したチャンネルに参加できるようになります。別の有料プランを利用していても問題はありません。一緒に仕事を進めるパートナーを Slack に招待してみましょう。要件を満たしているパートナーは、Slack プロプランを 90 日間無料で試すことができます。*
> ---
>  *詳細
>  対象となるチーム
>  対象となるチームは、Slack フリープランを使用している（Slack コネクトのトライアルを体験したことがない）チームと、初めて Slack を使用するチームです。Slack アカウントやワークスペースは、サインアップ時に作成できます。
>  対象となるチームは、Slack のプロプランとそのプレミアム機能（Slack コネクトなど）を 90 日間利用できるようになります。
>  トライアルは、各ワークスペースにつき 1 度だけ利用できます。


---
全体最適の解としてはそもそもこのシングルチャンネルゲスト、サイボウズの業務の一環としてやってるのだから、サイボウズワークスペース内にチャンネルを生やすべきだった

---
夕食食べてから整理しようと思って放置してたらいつの間に解決してた
つまり「インバイトした側がチャンネルに追加するまで、インバイトされた側はシングルチャンネルゲストとして上手く接続されたかどうかわからない」ということ？？
