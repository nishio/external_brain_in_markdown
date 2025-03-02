---
title: "2023-04-10 LLM Meetup"
---

`LLM Meetup Tokyo #1`
- [イベント案内](https://lu.ma/llm-meetup-tokyo-1)

> [takahiroanno](https://twitter.com/takahiroanno/status/1645426627780947969) 都内某所で行われたLLM meetupに行ってきたけどめっちゃ良かった。参加者は全員LLM関連のデモ持ってこないと参加不可というハイブローなmeetupだったんだけど、50人ぐらいきてた。参加者がひたすら蒸留されてて、LLM無職がたくさんいた。一つの時代のはじまりを感じたよおれは
- > [takahiroanno](https://twitter.com/takahiroanno/status/1645427231710416898) LLM無職=LLMの凄さを目にして思わず会社を辞めた人（最近起業した人を含む）
- > [takahiroanno](https://twitter.com/takahiroanno/status/1645432162223788032) この回ですね。来月もやるらしいので期待しております
- ![image](https://gyazo.com/73a9ab870d710714056d12ac43c69e91/thumb/1000)
    - [イベント案内](https://lu.ma/llm-meetup-tokyo-1)


## レギュレーション
> LLMをAPIを通して使った、fine-tune してる、作っているなど、実際に手を動かしてLLMを触っている人だけの小規模なミートアップです。後半のデモタイムで自己紹介＆デモをしていただける方だけ、ご参加いただけます。

# 自己紹介
![image](https://gyazo.com/eff4903533bee8c0410d86acf726e270/thumb/1000)
[[自己紹介]]

![image](https://gyazo.com/0065adb8c19478da2c88598da7dfc889/thumb/1000)
[[エンジニアの知的生産術]]
[[コーディングを支える技術]]
[[word2vecによる自然言語処理]]

![image](https://gyazo.com/a2fd1653cff19dce74331dfb829b9a16/thumb/1000)
3/8 [[自分のScrapboxをChatGPTにつないだ]]
- はるか昔のような気がする
    - 3.5
    - ChatGPT API
    - 3/9 [[Scrapbox ChatGPT Connector]]

![image](https://gyazo.com/a31e54ab3d757b4d6f9592716f17effe/thumb/1000)
3/18にGPT4 APIが来た
- [[中高生のためのChatGPT]]
- [[新しい自然]] [[誰も正解を知らない]]
    - [[みずからの目で見なければならない]]

![image](https://gyazo.com/6750c9f87d1c3bcd996e6d024216bbee/thumb/1000)
- [[ChatGPT Plugins実験]]


#  参加者のTweets
> [@kenn](https://twitter.com/kenn/status/1645424766864728066?s=20): LLM Meetup Tokyoめちゃ楽しかった！皆さんありがとうございました！

> [@elmer_mmm](https://twitter.com/elmer_mmm/status/1645427077976567808?s=20): LLM Meetup Tokyo #1 のデモでお見せした #ChatGPT でロボット動かしてみた動画です！会場では音が聞こえなかったので是非！他にもカチャカに乗せたり多言語話させたりしてます！

> [@yamaguchi_man](https://twitter.com/yamaguchi_man/status/1645433012140793856): LLM Meetup Tokyoよかった〜検索の部分色々皆さんトライされてるの知れて勉強になった
> ウチの場合だとルールベースとかと組み合わせてやっつけてる感じだからなあ

> [_mkazutaka](https://twitter.com/_mkazutaka/status/1645443396818079744) LLM Meetup Tokyo参加してきました！楽しかった！直接プロンプトどうなってるんですかとか語り合えるの最高だった！

> [wroorurkwao](https://twitter.com/wroorurkwao/status/1645422069457518593) LLM meetup にて、競争優位性は何が残るのかなぁ？みたいなことについてお話ししました。


> [y_matsuwitter](https://twitter.com/y_matsuwitter/status/1645467743788081152) 本日のLLM Meetup Tokyo #1 の資料。とても雑ですがMacBookProでも動くような軽量なLLMでAgentを作ろうとするとどうなるのかといったことを土日に実験していました。
>  ![image](https://pbs.twimg.com/card_img/1645467604910510080/Wu3yWlJC?format=jpg&name=medium#.png)
- > [y_matsuwitter](https://twitter.com/y_matsuwitter/status/1645469554573971456) 小さなモデルとはいえ、ReActのPromptは英語ベースなのでカテゴリとタスクを双方絞ってFine-Tuningすればもう少し上手く動いてくれるんじゃないか思っておりGPT-3あたりでデータ作ってColab上でFine-Tuningしてみるというのは次やってみたいところ。
> [erukiti](https://twitter.com/erukiti/status/1645377840790241281) 次は OepnAI パーカーを着てる y_matsuwitter さん
>  「Agentと軽量モデルの検証」
- > [erukiti](https://twitter.com/erukiti/status/1645378192923041792) 「LLMやりたいからチーム立ち上げた（自分とMLチームで）」
- >  パワフルや
- > [erukiti](https://twitter.com/erukiti/status/1645378327635697664) 「国策で日本LLM作りたい」
- >  「大企業さん意外に渋い」
- > [erukiti](https://twitter.com/erukiti/status/1645379093058449408) 「LLM Meetup くるような人は、自立的に動くagentに興味持ってる人多いやろ」
- >  はい
- > [erukiti](https://twitter.com/erukiti/status/1645379633121218560) 「LangChain とか agent をガシガシ組み合わせるとレスポンスまでの時間がかかりすぎる」
- > [erukiti](https://twitter.com/erukiti/status/1645380011309010945) 「今日の本題は、LLaMA.cpp とか Alpaca とかで ReAct できないか？」
- >  「結論としては現状のフリーの軽量モデルだと無理」
- >  Vicuna 13B 4bit や RWKV とかも無理っぽい
- > [erukiti](https://twitter.com/erukiti/status/1645380375835967488) 個人的には ReAct やるためのデータセットを GPT-4 とかで生成しまくって、fine-trune すればいいんじゃね？という気はしてる

> [chiral](https://twitter.com/chiral/status/1645430479959781376) 今日のプレゼンスライド置いときます。みんなイケてる発表ばかりでショボいけど、まぁ僕も実装してるぜアピールってことで笑drive.google.com
>  LLM Meetup Tokyo `#1` Masayuki Isobe.pdf

> [yakigac](https://twitter.com/yakigac/status/1645445493047300097/photo/1) LLM meetupで発表してきたスライド↓
>  [https://docs.google.com/presentation/d/1GqrGrd5aV3HxT_lNryOwTGpOaKsiDj-88jnV17QqjoM/edit?usp=sharing…](https://docs.google.com/presentation/d/1GqrGrd5aV3HxT_lNryOwTGpOaKsiDj-88jnV17QqjoM/edit?usp=sharing…)
>  ![image](https://pbs.twimg.com/media/FtXCFC9aMAA57RR?format=jpg&name=small#.png) ![image](https://pbs.twimg.com/media/FtXCI-zaMAAnkEy?format=jpg&name=small#.png) ![image](https://pbs.twimg.com/media/FtXCMrtaMAAjvR7?format=jpg&name=small#.png) ![image](https://pbs.twimg.com/media/FtXCQVKaIAAreXq?format=jpg&name=small#.png)
- > [yakigac](https://twitter.com/yakigac/status/1645447939769397248) そしてデモサイト
- >  [https://yakigac.github.io/role-flow/](https://yakigac.github.io/role-flow/)
- > [yakigac](https://twitter.com/yakigac/status/1645450320049487872) バグはこちらにプルリクお願いします。
- >  [https://github.com/yakigac/role-flow](https://github.com/yakigac/role-flow)

> [masa_kazama](https://twitter.com/masa_kazama/status/1645422048238538752) LLM Meetupで、「微分可能な検索インデックス」というタイトルでLTしました。キーワード検索やベクトル検索とは違う生成時代の新しい検索手法は楽しみですね。
>  ![image](https://pbs.twimg.com/card_img/1645058959131447297/fRc3IxD8?format=jpg&name=small#.png)
- > [masa_kazama](https://twitter.com/masa_kazama/status/1645422307043852289) 手法の詳細はこちらの解説記事が、とても分かりやすいです。
- >  ![image](https://pbs.twimg.com/card_img/1645423319636926465/Umee9ci2?format=png&name=medium#.png)

> [@AkihisaShiozaki](https://twitter.com/AkihisaShiozaki/status/1645320688746762242): OpenAI社のサム・アルトマンCEOが来日し、自民党・AIの進化と実装に関するPTに出席。日本での活発なChatGPTの利用などを引き合いに「日本がAIの利活用を通じて世界で大きな存在感とリーダーシップを発揮してほしい」と同氏。日本への期待を込めて、以下の7点の提案がありました。
> 1…
> ![image](https://pbs.twimg.com/media/FtVacYlaAAIdjh9.jpg)
- > [@overlast](https://twitter.com/overlast/status/1645362088934789127?s=20): この7つの提案は全て日本国内の4年先の技術力を削ぐ提案になっていますね。そして削ぐ力はそれぞれ違いますね。この提案の様なことを国内で実施できる様にしたいですね。またOpenAIが提案内容を一営利企業として実施し、各施策を日本の政府や自治体が優遇しないなら、単に便利、なので問題なさそうです

> [chiral](https://twitter.com/chiral/status/1645055988331077634) 明日のLLM Meetup Tokyoの準備だん。ヘルプデスクAI（EmbeddingsAPI,Weaviate,CompletionAPI, 社内PCでdocker-composeで諸々ホスト）と、LINEチャット占いAI（LangChain,Flask. ngrok使ってcolabでホストしてLINE MessagingAPIにつなぐまで）の、豪華（笑）2本立て！

> [tdualdir](https://twitter.com/tdualdir/status/1643497897269547008) こちらに参加します！！
>  GPTを使ってテーブルデータの前処理を自動化するデモをします！！（将来的にMatrixFlowに載るかも。）

> [@erukiti](https://twitter.com/erukiti/status/1645567650565857280): [https://t.co/VWJnFLhgia](https://t.co/VWJnFLhgia)
> LLM Meetup Tokyo #1 の飛び込み枠で発表したスライドです

> [npaka123](https://twitter.com/npaka123/status/1643478331512492033) 来週の LLM Meetup Tokyo 参加します。
>  ![image](https://pbs.twimg.com/card_img/1641079402430881792/eHGFgpqt?format=png&name=medium#.png)
[[2023-04-10 LLM Meetup]]

