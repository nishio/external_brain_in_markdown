---
title: "LLMと正規表現"
---

> [@nishio](https://twitter.com/nishio/status/1633284435952144386?s=20): 多くのプログラマーにとって[[手続型]]でないパラダイムに触れるのは[[正規表現]]なんじゃないかと思う。どういうパターンのものにマッチして欲しいかを記述して、具体的にどうするかは正規表現エンジンに任せる。[[LLM]]がプログラムに組み込まれていく流れも似たものになる。
> 正規表現エンジンに「正規表現」という謎の文字列とデータを渡したらマッチオブジェクトが返ってくるように、LLMに「プロンプト」とデータを渡したらレスポンスオブジェクトが返ってくる、現状でも大差ないな

> [@koizuka](https://twitter.com/koizuka/status/1633289420102307840?s=20): 正規表現のライブラリが標準で搭載された言語のように、大規模言語モデルを搭載したプログラミング言語が出てくる…？
- > [@nishio](https://twitter.com/nishio/status/1633291380629061633?s=20): @koizuka 現状はまだ手元で動かすのが現実的でないのでAPIを叩くのだろうけど、いずれ正規表現エンジンにフラグを渡して挙動を変えるみたいな感じで手元でやるかクラウドでやるか変えるようになりそう
- > [@ajiyoshi](https://twitter.com/ajiyoshi/status/1633290699188899842?s=20): hello worldのバイナリサイズが30GBになる未来
- > いやまあでも普通にそうなりそう。
- >  LLMがランタイムに組み込めるようになった当初は使わないコードではリンカが削ってくれたりするかもしれないが。
- >  そのうちに「面倒だしたった30GBなら常に同梱すればよくね？」ってなる。
    - > [@nishio](https://twitter.com/nishio/status/1633292065353392128?s=20): @ajiyoshi 「このプログラムをコンパイルするときには`libllm.so`をリンクしてください」「やだよめんどくさいよ1バイナリで完結しろ」という流れがいずれ起きそう…
        - > [@ajiyoshi](https://twitter.com/ajiyoshi/status/1633292205778690048?s=20): @nishio 確実にそうなりますねｗ

> [@ooharak](https://twitter.com/ooharak/status/1633326421128142848?s=20): @nishio 個人的にはですが、正規表現を知った時よりも[[SQL]]を知った時に手続き型との違いを感じました。
- > [@nishio](https://twitter.com/nishio/status/1633326885395656704?s=20): @ooharak 確かにSQLの方がしっかりと構文があるから「別の言語だ」感が強いですね。
