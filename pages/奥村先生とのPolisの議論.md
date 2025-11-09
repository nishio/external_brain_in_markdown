---
title: "奥村先生とのPolisの議論"
---

> [nishio](https://x.com/nishio/status/1954213468170760499) Polisの質問が多過ぎて途中で離脱したってのはよくあるリアクションだけど、Polisは人が途中で離脱することを想定した設計になってるので全ての質問に答える必要はないし、全ての質問に答えない人がいることが問題だと思ってもいない。むしろ離脱したほうがいいという考え方もできる
>  >nishio: 途中で離脱する人がいるのは想定済みのアルゴリズムで、情報量多い方から表示するアルゴリズムになっています。その1問に要約できるかどうかはデータで明らかになると思います。その意見を投稿して他の人がどのように反応するかを見ることもできます。

> [nishio](https://x.com/nishio/status/1954214377290170715) 離脱する人はこのトピックに対しての他人の意見を見ることに興味がないから離脱するわけなので、そういう人を無理に議論に参加させない方がよい、という考え方

> [h_okumura](https://x.com/h_okumura/status/1954343124886835587) 提示順序はランダムじゃないんですね。そうすると後の方まで答える人は特定の層で、バイアスがかかった結果になりそう。あと離脱は無答と区別してNから引くようになっていましたっけ？

> [nishio](https://x.com/nishio/status/1954347063669571728) 無作為ランダムではないですが固定でもないです。一人一人異なった順番になっています。なので投稿順序が後の方の質問にバイアスがかかることはないとと思います。

> [nishio](https://x.com/nishio/status/1954347370264842668) 離脱と中立回答は区別されていて、離脱は詳細レポートでは白、中立の回答は灰色で表示されています。離脱は割合表示の分母からは除かれます。
>  行列計算の際には欠損値は他の回答者の回答の平均で埋められます。

> [h_okumura](https://x.com/h_okumura/status/1954350362825224652) ありがとうございます。無作為でないからバイアスが生じるけれど完全固定ではないのでバイアスは少ないということですね。他の回答の平均で埋めるのは微妙ですが（中心に寄ってしまう）

> [nishio](https://x.com/nishio/status/1954426786638668242) もっと正確にいうと、各人のベクトルを各人の回答数Nの平方根あたりで補正していた気がします。

> [h_okumura](https://x.com/h_okumura/status/1954428325889233111) そうなんですね。[https://compdemocracy.org/algorithms/](https://compdemocracy.org/algorithms/) を読めばわかるのかな（なかなか面倒）

> [nishio](https://x.com/nishio/status/1954487732325253219) コードがClojureで書かれててかなり面倒でした。AIに解説させたものはこちら
>  [[Polisの質問提示順序の仕組み]]
>  この説明だけだとExtremityの計算方法がよくわからなかったです。
>
>  論文の形になってるものはこちら
>
>  [https://www.e-revistes.uji.es/index.php/recerca/article/view/5516](https://www.e-revistes.uji.es/index.php/recerca/article/view/5516)
>
>  こちらはアルゴリズムの詳細までは書いていないです



[h_okumura](https://x.com/h_okumura/status/1954343124886835587)
The presentation order isn’t random. In that case, the people who keep answering all the way to the later items would be a particular subset, so the results could end up biased. Also, was it the case that you distinguish dropouts from non-responses and subtract dropouts from N?

[nishio](https://x.com/nishio/status/1954347063669571728)
It’s not purely random, but it’s not fixed either. Each person sees a different order. So I don’t think the items that appear later suffer from position-based bias.
Dropouts are distinguished from neutral responses. In the detailed report, dropouts are shown in white and neutral responses in gray. Dropouts are excluded from the denominator when percentages are displayed. In the matrix computations, missing values are imputed with the average of other respondents’ responses.

[h_okumura](https://x.com/h_okumura/status/1954350362825224652)
Thanks. So there is some bias because it isn’t random, but since it isn’t completely fixed the bias is small—got it? Imputing with the mean of other responses is a bit questionable (it pulls things toward the center).

[nishio](https://x.com/nishio/status/1954426786638668242)
More precisely, I recall that each person’s vector is adjusted by the square root of their number of answers N.

[h_okumura](https://x.com/h_okumura/status/1954428325889233111)
I see. Maybe it’s explained if I read [https://compdemocracy.org/algorithms/](https://compdemocracy.org/algorithms/) (though that looks like a slog).

[nishio](https://x.com/nishio/status/1954487732325253219)
The code is written in Clojure, which made it pretty painful. Here’s an explanation I asked an AI to write:
[https://gist.github.com/nishio/3278475028844af3a896d86dddcdd9a1](https://gist.github.com/nishio/3278475028844af3a896d86dddcdd9a1)
Even with that, I still couldn’t quite figure out how “Extremity” is calculated.

Here’s a paper-style write-up:
[https://www.e-revistes.uji.es/index.php/recerca/article/view/5516](https://www.e-revistes.uji.es/index.php/recerca/article/view/5516)
This one doesn’t go into the algorithmic details.