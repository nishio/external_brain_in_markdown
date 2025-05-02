---
title: "webtiling"
---

ウェブページをタイル表示するアプリケーション
[https://github.com/nishio/webtiling](https://github.com/nishio/webtiling)
- 実装内容:
    - JSONによる設定ファイル（config.json）
    - [[Electron]]を使用したウィンドウ管理（WindowManager）
    - タイル表示機能（TileManager）
    - オフセット制御機能（OffsetController）
    - 設定ファイル読み込み機能（ConfigLoader）

- 別のconfigファイルを指定して起動：npm run start:custom test-config.json






[[Vivaldi]]には[[タブタイリング]]の機能があるが、[[XREAL One]]で使おうとしたときあんまりカスタマイズできなかった
- [[VivaldiのTab Tilingでワイドモニター対応]]
- XREAL Oneの[[横長ワイドスクリーン]]は3840 × 1080 ピクセル
    - 1/3にすると中央はCosenseを見るにはちょうど良い、Devinのようなサイドバーのあるものをやるには狭いって感じ
    - そもそも中央がメインの作業エリアでサイドはサブなのだからもっと狭くていいよね
        - 一応ドラッグして変えられる
    - YouTubeを小さい画面で流そうとか思った時にカラムの分割だけだと無駄な空間ができる
        - サイドだけカラムをさらに上下に分割するとかできるといいのかな…
- ChromeのWindowを複数出して好きなサイズで並べればなんとでもなる
    - が、そもそもそれは個別のアプリだと解釈されてるのでXREALを解除した時にぐっちゃぐちゃにデスクトップに戻される

[[Devinクレジット使い切り4/26]]の時にカジュアルにDevinになげたらあっさりできた
- > Electron+BrowserViewで複数のウェブページを任意のタイリングで表示するツールができたぞ()

2025-05-01
- 意外と問題なく動いてる

2025-05-02
- Scrapboxに入るためにGoogleログインをしてみた
    - 未知のアプリなので二要素認証を求められる、それはそう
    - 毎回だと面倒だと思ったが、次の起動では問題なくログイン状態で立ち上がった
    - もしかしてAIに認証の必要なサイトを読ませる的な目的で使える？
- 気づいた細かいことをDevinに頼んでおく
    - [https://app.devin.ai/sessions/cf0a515c5069470d91a821bc291be6b3](https://app.devin.ai/sessions/cf0a515c5069470d91a821bc291be6b3)
    - [https://app.devin.ai/sessions/00598fe10c224efb9542b86c4c61e274](https://app.devin.ai/sessions/00598fe10c224efb9542b86c4c61e274)
