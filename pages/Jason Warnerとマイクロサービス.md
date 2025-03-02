
Jason Warner(Now: MD @redpoint, Prior: CTO @github, @heroku, @Canonical)が[[マイクロサービス]]についての考えをツイートしたところ「GithubのCTOが『マイクロサービスは失敗だった』と言っている」みたいに一部分だけ切り取ってバズった。そういうのは本当に良くないのでちゃんと全文を読もうよと言うことでまとめた。

意味の塊ごとに英文→和文の順で書く。和文は和文だけで読んだときの理解度を優先して表現を変えたりジョークを削ったりしている。
- <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>この形式で西尾の注釈を入れている

> [@jasoncwarner](https://twitter.com/jasoncwarner/status/1592227285024636928?s=46&t=Ms0tUQCH9dgKUgj7oZ3kEw): I'm convinced that one of the biggest architectural mistakes of the past decade was going full microservice
> On a spectrum of monolith to microservices, I suggest the following:
> Monolith > apps > services > microservices
> So, some thoughts
過去10年間のアーキテクチャ上の最大の間違いの1つは、完全なマイクロサービスに移行しようとすることだと確信しています。
モノリスからマイクロサービスまでのスペクトラムで、私は次のように提案します。
モノリス＞アプリ＞サービス＞マイクロサービス

> [@jasoncwarner](https://twitter.com/jasoncwarner/status/1592227287532904448?s=20&t=BmC71gSmsFXzl6cP845XgA): First, these are thoughts, not rules. Anyone that has built a large distributed system knows they don't really work that way and have to adapt with it
> Second, stage will be important. If you are reading this at a 5-50 person company...just stick with a monolith. Trust me
> [@jasoncwarner](https://twitter.com/jasoncwarner/status/1592227289986580480?s=20&t=BmC71gSmsFXzl6cP845XgA): If you are reading this at a 10k person company, likely have all of these to some degree but here is where my quick thoughts might differ from what has been done in the past

- まず、これは考え方であって、ルールではありません。
    - 大規模な分散システムを構築したことがある人なら誰でも、それが設計時に考えたようには機能せず、調整しなければならないことを知っています。
    - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>最適な設計は事前に「この場合にはこうするべき」みたいなルールで決まるのではなく、実運用によって得られる知識に基づいて事後的に明らかになる、ということ。
- 第二に、ステージが重要です。
    - もしあなたが5～50人の会社でこれを読んでいるならば、モノリスにこだわるべきです。私を信じてください。
    - もしあなたが1万人規模の会社でこれを読んでいるなら、おそらくこれら(モノリス＞アプリ＞サービス＞マイクロサービス)すべてをある程度は持っていると思います
    - が、私の簡単な考えは、御社で過去に行われたものと異なるかもしれない

> Now, diversion. Let's talk definitions. There exist no exact definitions for these all
> services - supporting apps/monoliths, core infra pieces, needed by lots of surface area, core compliance func, possibly not written by app teams (infra maintains them)
>  microservices - few hundred lines of code, mostly one-offs, likely could/should be library or SDK

さて、定義の話をしましょう。これらのすべてに正確な定義が存在するわけではありません

- サービス
    - アプリ/モノリスをサポートするものです。インフラのコア部分です。
    - 多くのサーフェスエリアで必要とされている。(<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>surface areaって何のこと指してるのかな??)
    - コアなコンプライアンス機能。
    - アプリチームは書かないかもしれない（インフラチームが維持する）
- マイクロサービス
    - 数百行のコードです。ほとんどが単発のものです。ライブラリやSDKになる可能性が高い/なるべき

> Ok, with all that out of the way, let's talk why
>  My thinking basically goes like this
>  Speed & risk
>  	A. It's generally easier for entire engineering teams to work inside one big app (think entire site in Rails app) than to reason about the ways in which microservices will fail
>  	B. distributed systems, which you will have as you grow no matter what, are hard enough to reason about with introducing dozens let alone hundreds of microservices that have their own risk profiles
>  	C. as you go fully micro, you need to introduce new concepts to handle the sprawl
>  	D. A big one. Each bespoke infra service or microservice is an extreme version of debt IMV. Code is debt, but services are extreme versions of that. Really think about about what that means for you. Prefer your debt to be literal points of highest leverage not nice to haves
>

さて、理由を話しましょう。私の考え方は、基本的に次のようなものです。

スピードとリスク
- A. エンジニアリングチーム全体が1つの大きなアプリの中で作業する方が、マイクロサービスがどのように失敗するかを推論するよりも一般的に容易である。（例: サイト全体がRailsアプリなど）
- B. 分散システムは、成長するにつれてどうしたって必要になる。しかし、独自のリスクプロファイルを持つ何十、何百ものマイクロサービスを導入することは、とても難しい。
- C. 完全にマイクロにするには、スプロールを処理するために新しい概念を導入する必要がある。
    - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>無秩序にどんどん増えていくマイクロサービスを管理し繋ぎ合わせるためのレイヤーが必要になるよね、ということ
- D. 重要なポイント: 私が思うに、オーダーメイドのインフラサービスやマイクロサービスは、技術的負債の最たるものです。コードは負債ですが、サービスはもっと負債です。
    - それが自分にとって何を意味するのか、よく考えてみてください。負債とは「あったらいいな」で負うべきものではなく、最も高いレバレッジを発揮するために負うべきものです。

> I think a challenge we dist systems engineers have is we really like to not have duplication so we see something being done in a few places and think "let's just pull this out and make a microservice out of it".
>  In theory this is fine. And if done for a few tens of instances, it is fine. When it goes to several dozen microservices or...way worse...across massive company boundaries (think one color service for all of Microsoft/Google/Apple) it becomes less technical and more org challenge
> And I know what I'm presenting so many feels like some false dichotomies but in practice I find there are definite tech challenges with microservices, but there are even more org challenges with them

私たち分散システムエンジニアが抱えている課題は、重複を避けたいということです。なので、いくつかの場所で行われていることを見て、「これを取り出してマイクロサービスを作ろう」と考えるのです。

理論的にはこれでいいと思う。そして、数十のインスタンスに対して行われるのであれば、それは問題ありません。

それが数十のマイクロサービスや、もっと悪いことには、巨大な企業の境界を越える場合（例えば、Microsoft/Google/Appleのすべてに1つのカラーサービスを提供すると考えてみよう）
- これは技術的挑戦ではなく、より組織的な挑戦になる。
- <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>Microsoft/Google/Appleのそれぞれが自社アプリに「色を選択する」という機能を持っている。「それをマイクロサービスに切り出せばコードの重複を避けられる」という主張は"理論上は"正しいが、実際にそれをやろうとすると各社が自分たちに都合のいい設計を主張する。利害対立するステークホルダーの意見を調整して合意に至らせる、っていう技術的というより政治的な頑張りが必要になる。
    - [[共通部分を共有する絵]]

多くの人が、私の主張を、[[誤った二項対立]]だと感じるだろう。しかし、現実に私が経験したことだ。マイクロサービスには明確な技術的課題があるが、それ以上に組織的な課題がある。

> And of all the things I worry about it's this
- >  First, infra (unless company is led by unusually with-it CEO) almost always gets short end of priority stick
- >  Second, too many services typically leads to a lack of ownership problem and boundary issues
- >  Third, you introduce even more tooling to deal with too many microservices
>  And most importantly, each microservice that could/should have been a library or sdk or something introduces production risk
>  more code is indeed overhead, more services is customer facing prod/experience risk. Both approaches have overhead/risk but the % distribution is diff

そして、私が心配しているのは、この点です。
- 第一に、インフラは（とてもITのよくわかっているCEOが率いる会社でない限り）ほとんどの場合、優先順位が低くなってしまう。
- 第二に、サービスが多すぎると、所有権の問題や境界線の問題が発生する。
    - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>どのチームがどのサービスの変更権限を持っているのか、境界はどこか、が曖昧になる。修正して欲しいけど誰に言ったらいいかわからないとか、複数のチームが互いに「修正の責任があるのはあちらのチームだ」と考えてボールが間に落ちるとかの問題が発生する。
- 第三に、多すぎるマイクロサービスに対処するために、さらに多くのツールを導入することになる。

そして最も重要なことは、ライブラリやSDKなどにできた/するべきだったマイクロサービスが、それぞれプロダクションリスクをもたらすということです。
コードが多いことは確かにオーバーヘッドですが、サービスが多いことは顧客が直面するプロダクション/エクスペリエンスのリスクです。どちらのアプローチにもオーバーヘッドやリスクはあり、その割合が異なるだけなのです。

> So this is typically what I recommend
>  1. Be a monolith as long as possible
>  2. Services start in infra for infra reasons, not app eng typically
>  3. If breaking out mono, break to large apps, not small services
>  4. Think that each new app is a virtual wall in your company
>  5. Prefer libraries to microservices where possible
>  The classic "we introduced a color service" is my favorite extreme example of where I would choose a library over a service. Yes extreme example but hey, it gets very talked about as quintessential example

というわけで、私がお勧めするのは、典型的な方法です。
- 1: できるだけ長くモノリスであること
- 2: サービス化はインフラチームによって、インフラ側の理由で始める。アプリエンジニア側が始めるのではない。
- 3: モノリスから脱却する場合、小さなサービスではなく、大きなアプリに分割する。
- 4: 新しいアプリは、社内の仮想的な壁であると考える。
    - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>アプリを増やすということは社内に新しい「コミュニケーションの妨げ」(壁)をもたらすと考えて慎重になるべきということ
- 5: 可能な限り、マイクロサービスよりもライブラリを優先する

「カラーサービスを導入した」という古典的な例は、私がサービスよりもライブラリを選ぶ極端な例として好きなものです。確かに極端な例ですが、真髄を突いた例としてとても話題になります。

> "But Jason, what about Amazon and Uber and ..?"

「でも、ジェイソン、アマゾンやウーバーや...はどうなんだ？」

> 1. Hey, you do you. I'm just saying what I've gone through in experience
>  2. If you have the success of Amazon when that mandate came down for services, go nuts
>  3. These are more guidelines than rules

1. おい、おまえはおまえのことをやれ。私は私が経験したことを言ってるだけです。
2. お前の会社が「Amazonがサービス化を義務づけた時」と同じように儲かってるなら、大いに結構なことだ
3. これらはルールではなくガイドラインです。

> 90% of all companies in the world could probably just be a monolith running against a primary db cluster with db backups, some caches and proxies and be done with it
>  For the 10% of companies that hit planet scale (no pun intended here Sam) it's gonna be art figuring this out
>  Distributed systems combined with scaling companies is so complex and so few people have done it that it's hard to draw specific lessons from those companies. Each context and instance is different. What I'm talking about here is more thoughts on how to approach the problems

世界中の企業の90%は、プライマリDBクラスタとDBバックアップ、キャッシュ、プロキシで動作するモノリスで済ますことができるだろう。
地球規模の10%の企業にとって、この問題を解決するのはとても困難なことです。
- (<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>「アート/芸術の域に達している」という表現)

分散システムと拡大していく企業の組み合わせは非常に複雑で、それを成し遂げた人は非常に少ないので、それらの企業から具体的な教訓を引き出すことは困難です。それぞれの文脈や事例が異なるのです。私がここで話しているのは、問題にどのようにアプローチするかについての考え方です。

> And going back to this
>  Monolith > apps > services > microservices
>  It's basically an approach to scale: be one big thing for as long as possible. Never overcorrect to too small of things, go through it as you grow (even hyper growth). This is for org and tech
>  Again, it's art

そして、これに戻る
- モノリス > アプリ > サービス > マイクロサービス

これは基本的にはスケールするためのアプローチである：
- できるだけ長く一つの大きなものであること。
- 物事を過剰に小さくしすぎるのではなく、成長に合わせて進めていく。(急速な成長の時も)
- これは、組織も技術もおなじである。

繰り返すが、これはアートである