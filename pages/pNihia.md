---
title: "pNihia"
---

2024-05-05
- このScrapboxを読むアシスタントのGPTsを作る
    - [[⿻Plurality Assistant]]が便利だったので
- サーバサイドはprivate repos: `nishio/vecsearch-service` にある
- uidを必須のparamとして取るので503になった、OpenAPI Specの側でrequiredにしたけど、サーバサイドを直してもよい

アイコン作成
![image](https://gyazo.com/88e13329336c6e03b4d9c8aa651f6415/thumb/1000)
なぜこのアイコンが良いと思ったのかは謎

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>「西尾泰和」について解説して

<img src='https://scrapbox.io/api/pages/nishio/pNihia/icon' alt='pNihia.icon' height="19.5"/>西尾泰和氏は、多角的な視点と柔軟な思考を持つ研究者であり、特に知的労働と生産性、AIに置き換えられない価値について深い考察を行っています。彼は個人やチームの生産性向上に寄与する方法を研究し、円滑なコミュニケーションを促進するソフトウェアの開発にも携わっています。西尾氏の研究は、働くという行為が単なる対価の獲得だけでなく、顧客価値を生み出すことに重点を置いています。

彼はまた、情報科学の若手の会に参加し、サイボウズラボで知的生産性の研究を進めており、東京工業大学の特定准教授を兼任しています。西尾氏の著書「エンジニアの知的生産術」も高い評価を受けています（from `[🤖🔁西尾泰和]`)

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>西尾泰和の思想について説明して

<img src='https://scrapbox.io/api/pages/nishio/pNihia/icon' alt='pNihia.icon' height="19.5"/>西尾泰和氏の思想は、主に以下の点に焦点を当てています：
- 多角的な視点と柔軟な思考：
    - 西尾氏は、様々な角度から問題を見ることの重要性を認識しています。彼は知的労働と生産性について研究し、AIに置き換えられない人間の価値について考えています。彼の研究と実践は、個人やチームがより生産的になる方法を探求しています。
- コミュニケーションの円滑化：
    - 西尾氏はコミュニケーションを促進するソフトウェアの開発に関わっており、「場」の提供を通じて人々がスムーズにコミュニケーションをとれるようにすることを目指しています。
- 働くことの本質：
    - 西尾氏は、働くことは単に対価を得るためだけではなく、顧客価値を生み出すことに重きを置いています。彼の視点では、仕事を通じて価値を生み出すことが重要です。
これらの考え方は、西尾氏が関与する多様なプロジェクトや彼の著作に反映されています。彼の思想は、現代社会で求められる柔軟性と多様性に対応する知的生産性の向上に寄与しています（from `[🤖🔁西尾泰和]`)。


まあ[[Done is better than perfect]]だからとりあえずこれでリリースするか(Ver.1.0)
[ChatGPT - NISHIO Hirokazu's Assistant](https://chatgpt.com/g/g-V6olZSQJI-nishio-hirokazu-s-assistant)


Ver.1.1 [[コーディングを支える技術]]と[[エンジニアの知的生産術]]をKnowledgeに積んだ

これをハブとして今までの色々なプロジェクトを再構築していこう。

Ver1.2リリース
> [nishio](https://twitter.com/nishio/status/1787087217095287103) 検索時に時々エラーになるなぁ、GPTsはデバッグしにくいのが問題
> [nishio](https://twitter.com/nishio/status/1787105265944535222) APIにuser IDの口があるんだけどGPTが何も知らないのに適当なUser IDを入れてくるせいで「そんなユーザはいない」というエラーになってた
>  そこは直したけどそれでも時々エラーになる、サーバ側は200なので多分レスポンスサイズ超過なんだろうと思う

> [nishio](https://twitter.com/nishio/status/1787108456077672802) あー、そうか、Plurality Assistantの方は実験的に100tokenと500tokenの混在になってて、こっちはその実験前の実装だから全部のヒットが500tokenなのか、謎は解けた

> [nishio](https://twitter.com/nishio/status/1787111091715416413) とりあえずGPT用にレスポンスで返す個数を1/5にした新しいAPIを作ってそっちを呼ぶように変えたのでエラーになることは激減したと思います
Ver.1.3

Ver.1.4
- GPTの判断に必要のないデータを捨ててコンパクトな結果を返すように変更
- 同一ページからチャンクを取らないように
> [nishio](https://twitter.com/nishio/status/1787117492026171718) 色々改善した
>  ![image](https://pbs.twimg.com/media/GM0d4Mhb0AA-0Ph?format=jpg&name=medium#.png)

![image](https://gyazo.com/d07787600db724125538c48f95fc6acb/thumb/1000)

2024-05-07
Ver1.5 名前の変更(Nihiaを名前に入れた)
Ver1.7 Prompt改善

