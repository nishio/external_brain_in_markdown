---
title: "BitNet"
---

2024-02-28
[1ビットLLMの衝撃! 70Bで8.9倍高速　全ての推論を加算のみで!GPU不要になる可能性も – WirelessWire News](https://wirelesswire.jp/2024/02/86094/)

前からあったよね感に関して
> [goto_yuta_](https://twitter.com/goto_yuta_/status/1762766893990240463) BitNet b1.58について、真の意味での1bitのBitNetは元から存在していて、今回発表された「BitNet b1.58」はその亜種みたいなもので、元の1bit BitNetが持ってたパラメータに0を追加したことで結果として扱う平均情報量が1.58になって「BitNet b1.58」ということか。
- なるほどね
- > [mr_bay_area](https://twitter.com/mr_bay_area/status/1762767949277155820) 1-bit LLMの話、なんか大昔にあった気がしていて多分この論文だと思うのだけれども、引用されてなかったよ
- >  Binarized Neural Networks: Training Deep Neural Networks with...


> [goto_yuta_](https://twitter.com/goto_yuta_/status/1762755172089090537) Githubに実装も公開されてて、アーキテクチャ図もあるけど、Transformerの部品にBitってつけてビット加算にしてるだけでやってることはまじで同じそう。
>  なんで精度上がるんや...
>  ![image](https://gyazo.com/c5dc75a94a586f2380d18f9ab4593308/thumb/1000)

>  >[goto_yuta_/status/1762753632028807552/photo/1](https://twitter.com/goto_yuta_/status/1762753632028807552/photo/1/status/1762753632028807552/photo/1) マイクロソフトが発表したBitNet、やばすぎて半信半疑ながらも真実ながら凄すぎて期待してしまう。
>  行列の中身を1ビット(0 or 1のみ)にして、行列演算に乗算が必要なくなって高速化させてるらしい。
>
>  高速化する理屈はわかるけど、論文によるとなぜか精度も向上してるらしい。
>  やばすぎて一旦様子見。

