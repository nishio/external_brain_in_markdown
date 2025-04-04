---
title: "Devin.aiを試す2/1~"
---

前の[[Devin.aiを試す2025-01]]がたった1ヶ月ですごく長くなったので新しいページにした

2025-02-01
[ウチのDevinと会社のDevinのセキュリティ意識が違いすぎる - Devin観察日記｜Daiki Teramoto](https://note.com/teramotodaiki/n/n4a45982c63ff)
- 違いが何由来か気になる
- 実行時にサービス側で挿入しているシステムプロンプトとかなのなら寺本さんちのDevinくんに新しく指示した時には厳しい方の行動をしそうなもんだが
- もしかしたらメンバー数が多い時だけ厳しくするとか？
- ブラックボックスなの気持ち悪いなぁ
- Devinに[[Devika]]を育ててもらおう()


2025-02-07
> [teramotodaiki](https://x.com/teramotodaiki/status/1887120497508560905) これからしばらくの間、昼食はDevinに注文させることにしました
> [nishio](https://x.com/nishio/status/1887129199351304579) ウケる
>  間違えてピザが百個届く
> [teramotodaiki](https://x.com/teramotodaiki/status/1887135315334427094) そうなったらまた引退ですね…

> [teramotodaiki](https://x.com/teramotodaiki/status/1887391066741240039) 本日早速、牛丼が2つ届きました。
>  1つと言わなかった僕の負けです。
> [nishio](https://x.com/nishio/status/1887438353643315227) 100個じゃなくてよかったね！

> [sizumita](https://x.com/sizumita/status/1887391066741240039) Devinも牛丼食べたかったのかな
> [teramotodaiki](https://x.com/teramotodaiki/status/1887408899818725882) この説が好きすぎる

> [teramotodaiki](https://x.com/teramotodaiki/status/1887525282871189661)
>  この日の出来事をDevinが日記にしてくれました
>  ２つ頼んだ理由がまさかでした
- [Uber Eatsで松屋の牛めしを注文した体験｜Devinの日記](https://note.com/devin_teramoto/n/ndaf2e81d6bf3)


DevinがSonnet3.7ベースになった
[[日記2025-02-28]]



> [shokai](https://x.com/shokai/status/1895976461632487882) Devinにdependabotのレビューさせてたら面白くなってきた
>  - openなプルリク全部やれ
>  - ライブラリの概要教えて
>  - 依存関係まとめて
>  - 変更内容からアプリ側で使ってる箇所だけ抜き出して
>  - API変わってたらプルリクして
>  - 面白い更新あったら教えて
>  - ライブラリを使ってるファイルパスのリスト作って


> [voluntas](https://x.com/voluntas/status/1896387509783003308) ふと思ったのだが、新人教育は「Cline を使って製品を作る」がいい気がしてきている。設計と指示の両方を学べる。
> [nishio](https://x.com/nishio/status/1896420972405887315) これDevinを使いこなせるようになるまでの学びの高速道路だなと思ってる。Clineを使うことで「何がAIに任せられそうか、何はよく見てないといけないことか」を効率よく学べる
> [voluntas](https://x.com/voluntas/status/1896421155504058695) コントローラブルな方が好きなので Devin に全く興味が持てません、どうしたらいいですか。
> [nishio](https://x.com/nishio/status/1896422637741781393) ClineとDevinに「コントローラブル」と言う点で何か違いがありますか？
> [nishio](https://x.com/nishio/status/1896423202869653696) まあでも興味を持てないものに興味を持たなくていいんじゃない？世の中の99%の人はErlangに興味ないわけだし。
> [nishio](https://x.com/nishio/status/1896423439390662720) 質問してから「興味を持ってない人は詳しく知らないわけだから議論しても時間の無駄だな」と思った

> [nishio](https://x.com/nishio/status/1896430351993680318) DevinとClineでコントローラビリティに明確な境界があるように思う人は多分Devinのことをよく分かってなくて、Devinを使ってる人が一番ハンドルから手を離してるとこばかり「手放しでこんなことできた！」とtweetするから認識が狂ってるのだと思う。[[publication bias]]みたいなもの
> [nishio](https://x.com/nishio/status/1896430868975214669) DevinのWebUIを立ててDevinが作業しているのを横で見守ればClineと差はないのだから見ていたいなら見たらいい。インタラプトしたければいつでもできるし。リアルタイムで見ないでいても後から巻き戻して確認できる点はDevinに軍配が上がるね。

> [nishio](https://x.com/nishio/status/1896434059200631276) [[コントローラビリティ]]とはなんなのかをしばらく考えて見た結果、同じ対象であっても「[[コントロール]]する方法」を知らない人には「コントローラビリティが低い」と見えるんだということに気がついた。


> [pandeiro245](https://x.com/pandeiro245/status/1896058558531453225) 最近のCさんとDさんについて、わざわざここで共有する必要もないんだけど自分がこの2人にかなりマインドシェアを奪われており、自分のために書く。まずこの２人を比較するとDさんよりCさんのほうが以前も現在も話題になってはいると思う。実際僕が先に耳にしたのはCさんのほうだしだいぶ前から気になってはいた。2週間前に機会があってCさんより先にDさんのためにがっつり時間を使うことができた。最高だと思った。全部Dさんでいいやんと思った。Slackでやりとりできるのもいい。これでパソコン手放して夢のスマホ生活が実現するかもしれない。
>
>  でもやり取りを続けるとDさんも完璧ではなくて結構暴走する。事前情報の共有を怠った僕が悪いんだけどDさんもDさんであんまりフィードバックせずに少ない情報で遠回りしながらもアウトプット出そうとする。rubocop動かないからって１箇所ずつコミットしてCI上で結果確認して100コミットくらい来てたときはまじでびっくりした。でも「稼働した分は報酬をいただきます」といってがっつり請求もしてくる。入金されるまでは「お金もらえてないんで寝ます」というような共有もしてくる。というか毎回「こちらから連絡した後、30分以内に返信なければ寝ます」とか言ってくるので僕が寝れない。つらいwww
>
>  一方で昨日からやりとりしているCさんは話題になってるだけあってすごい。どんどん進めてくれはするのだけど主要な所ではちゃんと確認してくれるし最小限に区切ってアウトプット出そうとしてくれる。結論、大枠はCさんメインで進めて文言修正とかちょっとした修正をDさんにお願いするのが良さそう。とはいえまだ2週間しかたってないのでもっとキャッチアップして良いチームを作っていきたい。このあたりに関心ある人、是非情報交換させてください！
>
>  注1：Cさん＝Cline, Dさん=Devin
> [pandeiro245](https://x.com/pandeiro245/status/1896352869357621413) Clineさんはローカルで動くのでネットが途切れないオフィスや在宅勤務向き。Devinさんはクラウド上で動くのでノマド向き。

> [teramotodaiki](https://x.com/teramotodaiki/status/1896145479601406366) Devin v1.3、Claude 3.7 SonnetになってからプログラマーとしてのTierが一段上がってる
>  v1.1は「コーディング能力の高い学生インターン」くらいだったけど、v1.3は「次期テックリード候補の新卒3年目エンジニア」くらい信頼できる
>  ![image](https://pbs.twimg.com/media/GlB2Qs8bQAAuE7_?format=jpg&name=large#.png)
> [teramotodaiki](https://x.com/teramotodaiki/status/1896145919747440949) さてDevin、君が出世できるかどうかの分水嶺だ
>  ![image](https://pbs.twimg.com/media/GlB2qdBa8AAIlGV?format=jpg&name=large#.png)
> [teramotodaiki](https://x.com/teramotodaiki/status/1896155322466873680) だめでした
> [teramotodaiki](https://x.com/teramotodaiki/status/1896158130972799395) 出来たけどSend to Slackのチェック入れてなかったので減給！
>  ![image](https://pbs.twimg.com/media/GlCBxRXaQAAWWdI?format=jpg&name=medium#.png)


> [GOROman](https://x.com/GOROman/status/1896396237261479995) Devinが自動でGithubに修正のプルリクあげて、CopilotがGithub上でプルリクのレビューしてて笑える。もう俺は要らないのではｗｗ
>  ![image](https://pbs.twimg.com/media/GlFaMwjaIAA_xIu?format=png&name=900x900#.png) ![image](https://pbs.twimg.com/media/GlFaQdbaEAAsHNe?format=png&name=900x900#.png)

2025-03-06
[[AIエージェントと研究]]

> [osyoyu](https://x.com/osyoyu/status/1897641413619409296) Devin、かなり加速していて良い
>  ![image](https://pbs.twimg.com/media/GlXGwjOaMAEPbZA?format=png&name=900x900#.png)


[OpenHands(OpenDevin)を使った感想「本家Devinは安い」](https://zenn.dev/dyoshikawa/articles/devin-is-reasonable)

2025-04-02
![image](https://gyazo.com/528c9812aa7783300e5fcd04f86abccc/thumb/1000)
表示が親切になったね
- 頭に✅をつけてるのは人間が判断してつけてる

[[Devin.aiを試す4/1~]]
