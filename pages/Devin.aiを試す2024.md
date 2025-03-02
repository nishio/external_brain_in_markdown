---
title: "Devin.aiを試す2024"
---

from [[Devin.aiを試す2025-01]]
Devin.aiを試す2024
<img src='https://scrapbox.io/api/pages/nishio/o1 Pro/icon' alt='o1 Pro.icon' height="19.5"/>o1 Proによる解説:
Devin.aiは、ソフトウェアエンジニアリング作業を支援するために設計された「自律型AIエンジニア」です。GitHubリポジトリと連携してコードを書き、テストし、PRまで生成できるのが特徴です。以下に要点をまとめます。
- コードの自動生成・編集
    - 言語やフレームワークの移行、既存コードのリファクタリングや小規模な改善を得意とし、PRレビューも手伝ってくれます。
- 環境構築と作業履歴のスナップショット
    - Devin専用のワークスペース(VSCodeやShellなど)を自動で立ち上げ、セットアップ手順を踏んだ状態をスナップショットとして保存します。再開時に同じ環境を呼び出せるため、作業のやり直しを減らせます。
- 体験談：活用のコツと課題
    - メリット: たくさんの雑務やリファクタを一気に片付ける提案をしてくれる。「大規模なコード修正」や「テストを含む環境構築」など人間が面倒なタスクを自動化しやすい。
    - 注意点: 大量の変更PRを投げてくることも多く、手動レビューが追いつかない場合がある。テストが整っていないプロジェクトでは誤ったコードを生成しやすく、最終的には人間側の環境整備・方針指示が必要。


## 体験談
2024-12-28
![image](https://gyazo.com/1a674167f872c0237a359e64b391f239/thumb/1000)

![image](https://gyazo.com/f4d62a710b18ebc96d2b86fed201f0d0/thumb/1000)
自分個人及び所属するorganizationからインストール対象を選ぶ
![image](https://gyazo.com/fda9204d477f41cd478f15514ce15301/thumb/1000)
> Also includes public repositories (read-only).
- もしかして基本的に公開リポジトリに書き込めないのか？
    - そんなことはなかった
- nishioのallにしておく

![image](https://gyazo.com/42a4a5a6e9906e2dbdf9cf9c17e3168f/thumb/1000)

---

![image](https://gyazo.com/ce5140d68c6ed834403ef96e3bc6d463/thumb/1000)
もしかしてSlack Organizationが必要？

![image](https://gyazo.com/65d4323d45bdc3c96c9b0b6302efaf2f/thumb/1000)
いや、できるな

![image](https://gyazo.com/b05aed49f3405dba4b3e743313238dcc/thumb/1000)

Connect with Cognition Teamとはなにか
![image](https://gyazo.com/673274c49271d0e1afb40bff5f00ec09/thumb/1000)
あー、たぶんシングルチャンネルゲストでサポートチャンネルに入るのかな
- ![image](https://gyazo.com/d2c00d8bd395f3cee75cb9986cf3a635/thumb/1000)
- あー、Slack Connectか
    - [Slack コネクトを使ってチャンネルで他社と連携する | Slack](https://slack.com/intl/ja-jp/help/articles/360035092414-Slack-%E3%82%B3%E3%83%8D%E3%82%AF%E3%83%88%E3%82%92%E4%BD%BF%E3%81%A3%E3%81%A6%E3%83%81%E3%83%A3%E3%83%B3%E3%83%8D%E3%83%AB%E3%81%A7%E4%BB%96%E7%A4%BE%E3%81%A8%E9%80%A3%E6%90%BA%E3%81%99%E3%82%8B)
- ![image](https://gyazo.com/800d688e8a1c0ae93818dd2035f152c9/thumb/1000)
    - どっちだろ... 誰をinviteしたらいいかわからないからpublicかな
    - ![image](https://gyazo.com/1c65953c2532fa75e84624f5db763378/thumb/1000)
    - ![image](https://gyazo.com/36be6960cacd68c0dc61d02cf7b3e25b/thumb/1000)
        - ここまで来て「Slack Proが必要」となった
            - invitationをうける側でも必要なのか〜
        - ![image](https://gyazo.com/7f0f8826e12a44bedfe77b36f2d58d87/thumb/1000)
        - ![image](https://gyazo.com/a966109744d38c918ab73aa2fab8789a/thumb/1000)
- slack proを使ってslack connectするのはDevinを試す上で必須ではなさそう、これはサポートとの連絡窓口だと思う

![image](https://gyazo.com/eeda0b6d19affa72dba65e8725afc0d6/thumb/1000)
- ちょっと何を言ってるのかよくわからないな
- ドキュメントに書いてるかな
- [https://docs.devin.ai/get-started/devin-intro](https://docs.devin.ai/get-started/devin-intro)
    - [https://docs.devin.ai/get-started/quickstart](https://docs.devin.ai/get-started/quickstart)
- 既存のリポジトリの中で公開してよくて、AIが掻き回しても問題ないやつを考える
    - [https://github.com/nishio/concatPages](https://github.com/nishio/concatPages) これにしよ
        - [[concatPages]]

![image](https://gyazo.com/5d0f6fdca9b0515919a7d2ce688787e4/thumb/1000)
- ![image](https://gyazo.com/8943c17cd10a50d429efb62de2768d37/thumb/1000)
    - マジかよ
    - remoteインスタンスでVSCodeが立ち上がってる、これはコストかかるな〜w
- ![image](https://gyazo.com/1c2744c7f9e28a0cc97de6e1b5e73231/thumb/1000)
- ![image](https://gyazo.com/be4c6a89ea55f33f8e001d71a9d9579f/thumb/1000)
md

```markdown
Verifying correctness
- When verifying your code, you should run lint with `npm run lint` and auto-fix with `npm run lint -- --fix`.
- You should generally not worry about running the code or local testing. Prefer to use the tests that are automatically run in CI as a feedback loop for your PRs.
- Assume that you are not able to run tests locally unless a human has deliberately provided verifiably working instructions. Generic instructions for testing in the README often do not work since you may require specific environment variables or other machine setup to be able to properly run tests.
    - If you are asked to run tests, a local dev server, or otherwise interact with a running application, you should tell the human user to update your Knowledge with verifiably working instructions on how to run tests in your environment.
    - You should primarily rely on both human review and CI to verify that your code is functionally and stylistically correct
- If you have in fact been provided with verifiably working instructions on how to run tests in your environment, then the bullet point about not running tests locally is not relevant (and humans editing this note should feel free to update this section).

Additional Notes
- This repository does not appear to have any specific formatting, linting, or dependency management instructions
- When making changes, focus on maintaining consistent style with the existing code
- Since this is a Japanese repository, consider including both English and Japanese comments/documentation in your changes
```

興味深い
- リポジトリを指定しただけなのに"Since this is a Japanese repository"とか書いてるからリポジトリの内容を読んで生成してるな

![image](https://gyazo.com/d982209cb1ed5da4b18c8c879f70b6f9/thumb/1000)
- あー、なるほど
- ここで生成した環境をVMのimageとして保存しておいてタスクが与えられたら起動するんだな
- だからStep 4のSet Up Your First Repositoryでこう書いてたんだ
    - > My Workspace resets to a saved state for every new session.

![image](https://gyazo.com/35c339c21d03a1cd84033ae6d2a987ba/thumb/1000)
- ここで他人のリポジトリを設定できるか
    - 検索がnishio/以下に限定されてるな...
    - 自分がアクセス権を持ってる他人のリポジトリも設定できないので、まず自分のところにforkする感じかな

![image](https://gyazo.com/a7dd7d15a00fd35fe3c827e2156d0d93/thumb/1000)
- 想像通りセットアップ後のsnapshotが保存されている

![image](https://gyazo.com/13ef150c78e241aaad864e1075736767/thumb/1000)

出した指示
> 追加機能案
>  1: 開いてるページ自体もtextareaに含める対象にしたい
>  2: textareaの変更時にclipboardに入れたい
>  それぞれの機能を開発してPRして
追加
> 指示通りばっちり。
>  1: 修正点: currentは先頭にあって欲しい
>  2: それを修正したらREADMEもupdateして
>  3: self-mergeできる？
作られたPR
[https://github.com/nishio/concatPages/pull/1](https://github.com/nishio/concatPages/pull/1)

![image](https://gyazo.com/2dc7e22018426da4029a909b21da0a1a/thumb/1000)

$500で250 ACUs/monthだから1ACUで2ドル300円くらいで、この作業に3ACUなので 900円ですね

![image](https://gyazo.com/0463d08ebc0ceae20cc4a62a2fcff165/thumb/1000)
- 何を学んだかのメモが見れるのいいなw

![image](https://gyazo.com/b5e8e8118c24575ca7087774abab3900/thumb/1000)
![image](https://gyazo.com/ecf107fa5c300f2b94317f0f49930d30/thumb/1000)
たぶんSLEEPしてない間も課金される
- VSCodeが起動できるくらいの仮想マシンを立ち上げてるわけなので。

他のrepoをつなぐ
現実的でそれなりにでかいサンプル
[https://github.com/nishio/anno-broadlistening](https://github.com/nishio/anno-broadlistening)
手動セットアップでこけた
- ![image](https://gyazo.com/0145435695e03413906055854854db4d/thumb/1000)
こういうのこそAIにやって欲しい
できるか聞いたらできるって言ったので任せた
> nishio: @Devin セットアップ自体をDevinに任せることはできる？READMEを読んでpip installしたりするところをやってもらって、トラブルを記録してREADMEを更新したり、セットアップ後のsnapshotを取ったりしたい
> Devin: はい、セットアップ作業を自動化し、その状態をスナップショットとして保存することができます。
まかせてみた
![image](https://gyazo.com/113ed709c5de0336858a0d55a74f520a/thumb/1000)
適切にPythonを3.12から3.10に変更してる
- ![image](https://gyazo.com/536f15ca6b70519180dc5fd12102f31d/thumb/1000)
    - すごい超大詠唱呪文だなw
![image](https://gyazo.com/43fad7295f3d61647f26b37294cf8f92/thumb/1000)
- 何を考えているか見えるアシスタント、クラウドソーシングで知らない人に業務委託するよりだいぶ安心だな

スナップショットの作成
To create a snapshot of the current environment, you'll need to:
1. Click "Create machine snapshot" from the dropdown menu at the top right corner of Devin's Workspace
2. Fill in:
- - Snapshot name (suggestion: "anno-broadlistening-ui-dev")
- - Description: "Development environment for anno-broadlistening UI improvements"
- - Startup commands: cd ~/repos/anno-broadlistening && git pull
Please let me know once you've created the snapshot, and I'll proceed with the UI performance improvements for the cluster detail view.
![image](https://gyazo.com/4b8c6f1537313ce19ae670e7d3947675/thumb/1000)
なるほど、管理画面の操作はDevinが自分でできないが、何をすればいいかは知ってるから人間に移譲してくるのね
- Workspaceに表示されてないがSnapshotにある
    - ![image](https://gyazo.com/cd07eeab95266048d88a80cf1d74e043/thumb/1000)
環境セットアップの費用、4.74 ACU、1500円くらい

![image](https://gyazo.com/86fef487aad3694227c6e3cefca9b9b6/thumb/1000)
- 相手によって振る舞いを変えることを覚えた新入社員

AIが作ったPR
![image](https://gyazo.com/4a4a9ed1e5e6538d4daa587f7e204fdd/thumb/1000)
レビューしていく
![image](https://gyazo.com/32a26ccb9d5b18b971b06a813d5dbdd5/thumb/1000)
これは確かに僕のケアレスミスだな、reuseされてて再実行の必要がない時にraiseしたら良くない

---

22:00
1日使いまくっての感想
![image](https://gyazo.com/4d1ea4ca45133d80c1c0050eaf893ac6/thumb/1000)
- AIが4つPRしてきている
- なぜかPRできてないものもある
- 具体的にどんなものか見たい人はこちら
    - [https://github.com/nishio/anno-broadlistening/pulls](https://github.com/nishio/anno-broadlistening/pulls)
    - いずれcloseする

AIがものすごい勢いで実装するので僕のレビュー待ちが溜まりすぎてボトルネック...

Devinに「リポジトリを見て適当に改善して」って言ったらいい感じに雑用をしてくれてるw
- ![image](https://gyazo.com/eb37b2e535c19512136c9a6a86010242/thumb/1000)
- ただ、この後作られたPRをレビューしたら細かい修正だけではなくDesktopとMobileのコンポーネントの一部共通化までやってて、ちょっとそれは手放しでマージできないぞ？となった

似たケース
- [https://github.com/nishio/anno-broadlistening/pull/5/commits/ddc155a820278924dd715b5c2de76023a6fe4cf7](https://github.com/nishio/anno-broadlistening/pull/5/commits/ddc155a820278924dd715b5c2de76023a6fe4cf7)
    - `any`を`() => void`にするのはビルド通ってるならwelcome
    - ariaを追加するのも、同じコミットでやるのはどうかと思うが単体ならOK
    - なんかuseEffectが消滅してるけど、どういうこと？
        - 何をやってるのか理解したいので他のごちゃごちゃした変更と一緒くたにしないで欲しい...

Q: Devinすごくない？
A: すごいと思うじゃん？たくさん上がってきたプルリクをレビューしてもう21時なのに一つも「よし、これをマージしよう」に至ってないんだよ()
- うまく活用するためのスキルが必要で、今日たくさん試してみてとりあえずこのやり方ではダメだという気持ちになったw
- 人間とAIのどちらが悪いとは言い切れないんだが我々の側が自動化テストを用意してないのでAIがテストされてないコードをバンバン投げつけてきてレビューする僕が死ぬ
- まあ流石にもうちょっと噛み砕いて親切に指示しないと無理か〜という気持ち
- あ、sys.argvを自前でパースするのをやめてargparse使えという指示は半分くらい期待を満たしてるな

AIの書いたコードを一つマージすることができた
- [https://github.com/takahiroanno2024/anno-broadlistening/pull/42](https://github.com/takahiroanno2024/anno-broadlistening/pull/42)

まだまだ「全部AIにまかせたらいい」という感じではない
- 「AIにそのままマージできるようなコードを作らせるためのノウハウと環境整備」を人間の側が頑張る必要がある
- 今日の実験で分かったこと
    - AIにテストでOpenAIのAPIを叩かれたくないから「やらなくていいよ」と言ったせいでテストされてないコードが量産されてしまった
    - どういう変更をした時にはどういうテストをすべきなのか、コストをかけずにテストするための中間データはどこにあるのか、などのドキュメント化やテストコード化が必要
    - テストが「コード」だけでなく「自然言語のドキュメント」でも実行できるようになったのは進歩

![image](https://gyazo.com/06213dad5ed528b9355313d3cc4abf75/thumb/1000)

Devinがこんな機能つけたら？と言ってくる
I recommend implementing the optional --retry-failed flag because:
1. It provides explicit control over retrying failed extractions
2. It complements the force_cache improvements by allowing targeted retries
3. It helps users distinguish between "use cache but retry failures" vs "use cache for everything"
4. The implementation cost is low since we already have the status tracking in place
Would you like me to proceed with implementing this feature?

Webアプリをデプロイしてくる
![image](https://gyazo.com/8749d78b295e7a9f0a5fee1febb2e882/thumb/1000)


> [teramotodaiki](https://x.com/teramotodaiki/status/1872644869140971604) めちゃくちゃ面白いですね。"やる気はあるけど先走って空回りするタイプ"のマネジメントとそっくりで…
>  「こういうプルリクを作られると私がレビューしづらいので止めてね」みたいなコミュニケーションがDevinにも必要なんですかね…w
> [nishio](https://x.com/nishio/status/1872649270584922235) >"やる気はあるけど先走って空回りするタイプ"
>  それだw
> [nishio](https://x.com/nishio/status/1872651578836148661) こういうの困ります、とねっとり説教したらちゃんと分割してくれますが、英語で捲し立ててきます()
>  ![image](https://gyazo.com/a17322d0997f4b1e90c3bcf98d12c3c6/thumb/1000)
> [teramotodaiki](https://x.com/teramotodaiki/status/1872654930978492766) おお〜っ絶対謝らないタイプの鋼メンタル属性だ！！いい性格してますねぇ〜、僕も雇いたくなってきた
>  どれだけ説教してもメンタルが鋼なので、心理的安全性がありますね！！

プルリクエストの作成にしばしば失敗する
- 「もう一回試して」と言えば成功することもある
    - 謎だね
- 諦めてpatchで送ってきたものをgit applyしたりする

今日のところは一旦「いろいろ試してみて体験する」という感じ
- ここからドキュメントをもっと読んだりとかAIが働きやすい仕組みを整えたりとかしていく感じ
- [Introducing Devin - Devin Docs](https://docs.devin.ai/get-started/devin-intro)
- 一通り読んだ


2024-12-28
タスクをやってる最中に上司が思いつきで色々言うと元々やってたタスクを忘れてしまう(それはそう)

昨日は無茶振り放置プレイをしてたので今日はマイクロマネジメントをしている
- 実は短期的な生産性だけを考えるとマイクロマネジメントした方がAIも人間も生産性が高いのかも
- しかしそれをやると自発的に考える力が育たないので長期的には害がある
- AIは現状のところそもそも自発的に考えないので上司の側にもその能力の成長機会をケアする必要がない

プランが条件分岐することもあるのか、なるほど
- ![image](https://gyazo.com/98b8314931841fd32827af557af11c86/thumb/1000)
- 確かにソースコードを書く能力があれば「条件分岐のある行動計画」も可能か

Devinが作業しているのを横で見ている、[[ペアプログラミング]]
- 「現状のREADMEを読んでハマる人」のshellやVSCodeを同期/非同期で確認できるってのは、むしろ超手軽な[[ユーザーテスト]]として解釈できる気がする

ふわっとした検証の指示で検証できてる
- 指示<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
    - 大規模なデータに関してはdata-aipubcomブランチに生成結果が入れてあるのでそれを使ってテストすると良いでしょう
    - 正しくテストできると点のたくさんある散布図が得られるはず
    - 散布図の点はたくさんある？
<img src='https://scrapbox.io/api/pages/nishio/Devin/icon' alt='Devin.icon' height="19.5"/>
> 散布図の確認が完了しました。多数の点が異なる色でクラスタリングされて表示されており、期待通りの可視化が得られています。具体的には:
> - 複数の色分けされたクラスターが表示されています
> - 各クラスターには多数の点が含まれています
> - 散布図全体で数千個の点が可視化されています
> 可視化は正常に機能していることを確認できました。
どうやって動作テストをすればいいかのドキュメントを作らせる、便利
- [https://github.com/takahiroanno2024/anno-broadlistening/blob/main/scatter/VERIFICATION.md](https://github.com/takahiroanno2024/anno-broadlistening/blob/main/scatter/VERIFICATION.md)


永続化のレイヤーが3つあるんだな
- 開発環境、セッションの開始とともにスナップショットからVMを作って割り当て、セッション終了後に捨てる
- スナップショット、いい感じにセットアップした状態で保存しておく
- 知識、セッションをまたいで維持され、適宜更新もされる

GitHub上にはソースコードが永続化されてるけど、実際にはそこから毎回環境構築をするのはオーバーヘッドが大きくて無駄だから開発環境は再利用したい
一方で開発環境が単一だったりユーザの手元の環境をそのまま使ってたりすると、確率で発生する誤操作で環境を破壊した時のデメリットが大きい、だから「綺麗な環境」から毎回スタートする
これらの色々なものをまたぐ、個別のセッションやプロジェクトよりも上位の存在として「知識」の層があって、そこに蓄積が起こることによってだんだん良いアシスタントになる


知識がストックされていく
- ![image](https://gyazo.com/d30a982fc39a28d084efaecba2da3a5b/thumb/1000)
- ちゃんと「過去の記憶のアップデート」もするようだ
    - ![image](https://gyazo.com/8b306a39a0ab9229caac4833474f510f/thumb/1000)
    - 「npm testがちゃんと整備されてないのでブラウザを開いて確認する必要がある」とかメモされているww


Advancedに入れられてるけどsnapshotの方が仕組みがわかりやすくて好きだな
- ![image](https://gyazo.com/4350a8a27023b46bb57982b30900c365/thumb/1000)
- snapshotを指定して環境構築させる
- うまくできたらそれをまたsnapshotとっておこう
- ✅


2024-12-29
Devinと1スレッドやりとりして寺本さんが契約を決意したw
from 未踏ジュニアチャット
- teramotodaiki
    - Devin買います
    - 本当にフルリモートのエンジニアを一人雇ったような感じの体験でした
    - 思ってたより仕事のやり方がちゃんとしてた。　指示を聞く→色々試す→こういう選択肢があるけどどうしますか？って聞く、みたいな
    - みなさんがインターンなどをする時もこういう振る舞いが求められると思うので、Devinの思考を観察するのは参考になると思う
        - [[思考プロセスが見れる]]
- nishio
    - Devinを見てコミュニケーションを学ぶのかww
- teramotodaiki
    - めっちゃそれあると思ったんですよね〜。今ってインターンとかしないと学べない事じゃないですか。でもDevinを雇うと「仕事させる側」を体験できる上に、Devinの思考を全部読めるので、「仕事うける側」としてのセンス上がると思う
    - まあ働き方は会社によりけりなので、Devinの真似をしたら水が合わない会社も当然ありますが
    - というわけで、みなさんも西尾さんのクレジットが余ってるうちにDevin借りたらよいと思います。中々ない機会なので…！
- nishio
    - たしかに。昔クラウドソーシングが出だした頃に仕事を外注で出す側を試してみて「誰を雇うか決める側」の経験がめっちゃ学びがあるなぁ〜と思ったのだが、AIアシスタントの登場で誰もが「仕事をさせる側」の視点を経験できるって効果もあるのか

> [@teramotodaiki](https://x.com/teramotodaiki/status/1872967504060129336): Devin観察日記 0日目｜Daiki Teramoto
>  [Devin観察日記 0日目｜Daiki Teramoto](https://note.com/teramotodaiki/n/n00dde86ff676?sub_rt=share_pb)
DevinはREADMEやテスト手順ドキュメントを作るのにとても有能
- 記事を見て「READMEの更新に2000円かよ」と思うエンジニアもいそう
- ドキュメントは軽視されがちだが、実際にプロジェクト固有の知識を持たないAIアシスタントや人間の新人がプロジェクトに参加するときに時に真っ先に必要になるものなんだよな
- マネージャー視点ではその整備は重要なものだし、時給2000円のエンジニアが1時間でできるのか、時給8000円のエンジニアが15分でできるのか、とか考えるとDevinにアウトソースできるのは組織視点では有益と思う
- ただし現時点ではシニアエンジニアがレビューしてるし、多分将来的にも完全無人運用にはならない。言語化されてなくてチームメンバーの中にしかない情報があるから。ここの部分のコストがどう乗ってくるかはプロジェクト依存な気がする
- 新人オンボーディングやテストやバックログがしっかり整備されてるプロジェクトほどAIアシスタントがすんなり活動できると思う

英語でドキュメントを作らせた
> [nishio](https://x.com/nishio/status/1873157831073116640) We, anno-team, have been actively developing anno-broadlistening, based on the source code of @AIObjectives talk-to-the-city-reports. In the spirit of open source, I believe it’s important to contribute our updates back to origin. However, our team is limited in time and resources, so we haven’t been able to provide detailed feedback or documentation in English until now. Today, AI created a document that highlights the differences between our Japanese version and the original English version. I hope this will help bridge any gaps and make collaboration easier for everyone.
>  私たちanno-teamは、@AIObjectivesのtalk-to-the-city-reportsのソースコードに基づいて、anno-broadlistening 積極的に開発してきました。オープンソースの精神に則り、アップデートをoriginにfeedbackすることが重要だと考えています。しかし、私たちのチームは時間とリソースが限られているため、これまで英語で詳細なフィードバックやドキュメントを提供することができませんでした。本日、AIは、日本語版と元の英語版の違いを解説するドキュメントを作成しました。これがギャップを埋め、すべての人にとってコラボレーションを容易にするのに役立つことを願っています。
>  [https://github.com/takahiroanno2024/anno-broadlistening/blob/main/DIFFERENCES.md](https://github.com/takahiroanno2024/anno-broadlistening/blob/main/DIFFERENCES.md)
こういうのはAIが得意そう。


<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>TypeScriptでのany → () => void とかPythonでの型アノテーションとかの付与は、その後テストして通ってるなら良いことだが、他の意味的変更を伴う実装に混ぜられるとレビューが大変なのでコミットを分けて欲しい。
<img src='https://scrapbox.io/api/pages/nishio/Devin/icon' alt='Devin.icon' height="19.5"/>承知しました。型アノテーションの変更は、意味的な変更とは別のコミットにまとめるようにします。
![image](https://gyazo.com/3350bf42e0e4cfe9b3baca32fdfcec8b/thumb/1000)


将棋の多面指しみたいな気持ちだ
- 2並列ぐらいが僕が安定してできるラインかなぁ
- まあペアプログラミングのドライバーは一個しかできないのでよりスケールしている

2024-12-30
![image](https://gyazo.com/0e51ecb063f192eefc2b461c144e5ff7/thumb/1000)
- "aipubcom"がdataset-aipubcomブランチに入ってる分析処理実行済みのデータセットを使うということだとドキュメントなどから理解している
- プロジェクトに対する知識が蓄積していくことによって、短い指示で意図通りに動くようになっていく

「思いついたアイデア」は、それをメモしておいても勝手には成長しないけど、月額$500払っといてDevinという苗床を作っといたら「Devinに投げつけるというメモの取り方」をするだけで勝手に詳細化・具体化されて行く、これはいいかもしれないな。
- プロトタイプはそもそも「素早く試して捨てるために作る」というけど、実際にはもったいなくて捨てられなかったり、他人に任せた場合に「書いたコードを捨てられたエンジニア」が不満に思ったりするところ、AIが書いてるなら捨てるのに躊躇いらない的な。

> [takahiroanno](https://x.com/takahiroanno/status/1873574200033890656) Devin観察を @nishio さんの周辺でやっているのですが、エンジニアのお仕事のしかたのパラダイムが変わりつつあるのを感じる。。。
> [takahiroanno](https://x.com/takahiroanno/status/1873689975470059563) エンジニアAIのDevin（月額$500）が入ったSlackでちょこちょこ作業を一緒にやってみた。これはすごい。まだアホなところが多いんだけどすごい。AIエージェントと共同する未来の職場が既に現実になっていた・・・！
>  ![image](https://gyazo.com/5105fb5ab1981869c08c1ab7bbf2b684/thumb/1000)![image](https://gyazo.com/db6213db907242692ce2bef23ff14e49/thumb/1000)![image](https://gyazo.com/ae4cebf6ad69f9ca4f4e7f8c0be5463a/thumb/1000) ![image](https://gyazo.com/7a5034becb2ac1bf6cf86d67ed135eb7/thumb/1000)
> [takahiroanno](https://x.com/takahiroanno/status/1873690019346755630) １年も経たないうちにこの新入社員はめちゃくちゃ戦力になってる気がする

> [takahiroanno](https://x.com/takahiroanno/status/1873693465890234831) Devinを使った第一印象として思ったことメモ
>  ・まだアホ（PRづくりに失敗）
>  ・でも賢いところは賢い
>  ・高学歴のピーキーな新卒感ある挙動に似ている
>  ・エンジニアが普段使っている媒体にめちゃくちゃ寄り添ってくれるのが良い（SlackとGitHub）。自分からChatGPTみたいな特設ページを開きいにいかなくても良いのがいい
>  ・特にエージェントの場合は数十分ぐらい作業してたりするから、普段づかいしているチャットツールとの相性が良い（通知に気づかないといけない問題）
>  ・普段使いしているチャットツール上で命令した場合、人間のチームメンバーが「Devinはこの辺苦手だよ」とかコミュニケーションに自然に入ってきてくれるのも良い
- 今回安野さんが始めたスレッドでは4人+AIでわいわいしてて、近い未来にこういう働き方がくるんだなぁと学びが大きかった、[[Devinを見る会]]をやった価値があった
>  ・対話の中で知見を獲得していくところがすごい良い（こういう細かい知識をユーザー対話の中で蓄積していくメカニズムはあらゆるエージェントで活用できると思う）
>  ・Gmail版のDevinが欲しい。割とすぐ出来ると思うんだよな。Gmail返信とかも上記の細かい知見（Aさんにはxxxxで返して）とかの積み重ねなので知見の自動蓄積はワークしそう
>  ・AIに暗黙知をどう教えこむか？という大きなチャレンジがあるなと思っていたんだけど、それはチャットツールと融合しながらチームで共同作業することでOJTで自然とAIに教えてゆけばいい、という解が提示されてて良かった
>  ・特設のDevinアプリ上のページの中を見るとDevinの頭の中（というか机の上）が見れるのも良い。エコシステムが整備されてきているのを感じる。TerminalもEditorもBrowserも見ることができるし、介入も出来る

> [takahiroanno](https://x.com/takahiroanno/status/1873694182617104721) AIエージェントを使うのは個人戦じゃなくてチーム戦なんだという気付きがあった
>  組織としてAIの利用を前提としたワークフロー、データの整備が出来ているかどうかでめちゃくちゃ生産性が変わりうるよね
- [[AIエージェントを使うのはチーム戦]]

寺本さんの続編
[Devin観察日記 1日目｜Daiki Teramoto](https://note.com/teramotodaiki/n/nd2f47ab20c26?sub_rt=share_b)

anno-broadlisteningの進捗
- できた！
- ![image](https://gyazo.com/e1e3c3830bc4cc856f047b551bdbd317/thumb/1000)
- 色覚特性に合わせたカラーセットの切り替え機能
- 安野さんがチャットで要件を話して、Devinがしばらく頑張ったけど完成させられなかったコードをとってo1 Proにデバッグさせて、そのo1 ProのコメントのあるIssueをDevinに渡して修正させた
- [https://github.com/takahiroanno2024/anno-broadlistening/issues/47](https://github.com/takahiroanno2024/anno-broadlistening/issues/47)
- Devinが自力でタスクを完了できなくなったら、できたところまでブランチにしたりIssueに書いたりして、それをo1 Proや人間がレビューしてアドバイスすればいい


> [nishio](https://x.com/nishio/status/1873740723771846874) 「24時間いつでもチャットに1分で返事し、雑なアイデアを投げつけられても実行プランを立てて実行し、そのプランや作業しているコンソール、エディタ、ブラウザをいつでも見られ、しかも録画されてパーマリンクが付いてシェアされる」という人権のない働き方をするエンジニアが時給1200円で雇える時代
> [nishio](https://x.com/nishio/status/1873741204229341562) 次の1年でのエンジニアの需給バランスの変化は去年思ってたのよりも何倍も速いということなんだよな
> [teramotodaiki](https://x.com/teramotodaiki/status/1873879852308455930) エンジニアにとってDevinが代替財か補完財かというのはケースバイケースになりそうですね
>  Devinをマネジメントする人は今のところまだエンジニアである必要があるので、「Devinを使って成果を出せるエンジニア」の需要が新しく生まれてそう


この3日間でDevinにやらせたことの一覧をo1 Proに作らせた
- [https://gist.github.com/nishio/e86ab242fed7881620f8006712f013e0](https://gist.github.com/nishio/e86ab242fed7881620f8006712f013e0)


[[会話と執筆のメタファー]]
- 結局のところ「レスポンスが帰ってくるまでの時間」や「どの範囲のタスクがどの程度のクオリティでできるのか」は使ってみることによって理解される、使う前の機体は実際の分布とマッチしていない
- その期待とのズレがあったときに修正できるかどうかが[[使いこなしスキル]]
    - 「[[他人に期待しない]]」の図を何年も前に書いた時には想定していたのは人間だったが、AIアシスタントにも同様に成立する


根拠ない憶測なんだけどPRを出せないのは「企業の非公開のorganization内での開発」を想定して訓練したせいでOSSでpublicなrepoを手元にforkしてるケースに不慣れで混乱してるんじゃないかな〜という気持ち
> (Devin)現在、以下の2つの選択肢があります：
> 1. nishioさんの個人アカウント下に作成（my-cosense-scripts）
> 2. nishio組織下に作成（nishio/my-cosense-scripts）
> どちらの場所にリポジトリを作成すべきでしょうか？
やっぱりorganizationではないアカウントなことに混乱してるな


2024-12-31
Devinはテストが通らなくなった時に不毛な試行錯誤を頑張ってしまう時がある
- 僕が俯瞰で見て「とりあえず一旦止まろうか」となる
- 自分の置かれた問題を解決するための適切なアクションが、選択肢の候補に含まれていないので一生懸命努力するけど不毛
- 改めて考えると人間もそうだという気がした


僕が紅白を見てる間、彼はずっと実装していた
- [https://github.com/nishio/my-cosense-scripts/commits/main/](https://github.com/nishio/my-cosense-scripts/commits/main/)


> [teramotodaiki](https://x.com/teramotodaiki/status/1873883310671487184) これ Devin Enablementがいるなぁ
>  Devinの特性を理解して、Devinの開発効率を上げるために、開発環境の整備を行う
>  たとえば
>  特性:DevinはOAuthでログインできない
>  整備:Devin用の認証手段を用意(E2Eテストがあれば流用できる可能性が高い)
>  開発生産性にコミットするからPlatformチーム？の役割になるのかな
> [teramotodaiki](https://x.com/teramotodaiki/status/1873883315482353722) Devinの開発生産性は
>  ・トラッキングしやすい
>  ・お金に換算しやすい
>  ・改善しやすい
>  ので、一瞬で激アツトピックになる予感


> [teramotodaiki](https://x.com/teramotodaiki/status/1873769338232320195) 「逐一やってること教えて欲しい、独り言みたいな感じで」ってDevinに言ったら、「thinking out loud style」ってメモしてた。それそれ！バイブス合うわ〜〜


新しく作ったリポジトリでも問題なくPRできてる
- [Commits · nishio/my-cosense-scripts](https://github.com/nishio/my-cosense-scripts/commits/main/)
- 一方でそのあとforkした別のリポジトリではあっさりPR失敗してるので、やっぱforkされたリポジトリの扱いに苦手があるっぽいな


> What happens if I don’t use my full ACU capacity?
> For Personal and Team plans, the ACU capacity included with your subscription resets each billing cycle. However, any additional ACUs you purchase will remain available as long as you have an active subscription.
とりあえず追加分は持ち越されるのがわかったので100ACU追加することにしました

このプロジェクト([[Devinを見る会]])を始めた時は「一人でクレジットを使い切るかどうか不明」「余らせるくらいならシェアした方が有益だし、複数人で同じものを見て議論できると有益」という気持ちだったのだけど、1週間ほど使った結果として来月以降も課金を続けてデフォルトの250ACUを使い切る感じになりそうだなと感じている。
このプロジェクトをどのタイミングでどう解体するかなーというのを今後考える必要がある。


DevinのGoogleアカウントを作るとか、むしろ自分のGoogleアカウントでGMail読んでくれとかしたくなる
- Devinのブラウザを操作してreCaptchaを突破したけど、「これは怪しい」と説明のないエラーで弾かれた
- 試行錯誤すると関連アカウントごとBANされかねない、諦めた
- AIにメールを読ませたければ、読めるメールサーバを立てて転送する方が良さそう
    - 自分でやらなくてもすぐGoogleがやるかサードパーティが提供する


大量のインスタンスを並列に作ると僕のタスク管理が破綻するので1つのインスタンスを長く使うスタイルになってきたけど、そうすると今度はスマホでスレッドをスクロールするのが面倒に…


Devinの書いたタスク管理のドキュメント面白い
- ![image](https://gyazo.com/dff8c7759b709e654d4eeff0692cb10d/thumb/1000)
- これprivate repoにしてたけど公開できた方がいいな、分離してもらおう
- > システムとデータの構造を確認しました。分離に関して以下の点について確認させてください：
- >  1. tasksディレクトリ内のdocs（task_format.md, system_overview.mdなど）は、システムの仕様を定義する重要なドキュメントです。これらは公開システムの一部として残すべきでしょうか？
- >  2. test_advanced.yamlはテストデータとして使用されているようです。これはシステムのテストに必要なファイルとして公開リポジトリに残すべきでしょうか？
- >  3. backlog.yamlには実際のタスクデータが含まれており、これは確実にプライベートリポジトリに移動する必要がありますが、その他のファイルについてご意見をお聞かせください。
- 確認してくるのえらい、1と2は公開するつもりだったが、確かに「システム」がどこまでなのかはあいまい


