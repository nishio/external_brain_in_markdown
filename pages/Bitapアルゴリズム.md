---
title: "Bitapアルゴリズム"
---

> Bitapアルゴリズムは、ビット演算の並列性を利用した文字列探索アルゴリズム
>  Baeza–Yates–Gonnetアルゴリズムや、Shift-andアルゴリズム・Shift-orアルゴリズムとも呼ばれる
>  [[あいまい検索]]に利用できることが、他の文字列探索アルゴリズムにない特徴である。
- [Bitapアルゴリズム - Wikipedia](https://ja.wikipedia.org/wiki/Bitap%E3%82%A2%E3%83%AB%E3%82%B4%E3%83%AA%E3%82%BA%E3%83%A0)
- > 'bitap' (bit-parallel approximate pattern matching)

- [[asearch]]で実装されている

まずシンプルな「あいまいでない検索」から説明
![image](https://gyazo.com/32dc88bb9200d0663c6cdc643ea29938/thumb/1000)
こういう直線状の[[NFA]]を使って文字列の受理を判断する
各状態にいるかどうかの1bitを整数にパックするとANDやシフトの演算を使える
この図の場合
- 初期状態 100
- 受理状態マスク accept 001
- 文字aに対応するマスク 100
- 文字bに対応するマスク 010
    - その文字で次の状態へ遷移する矢印の生えている根元の状態にビットが立っている
- 状態の更新: `state = (state & mask) >> 1`
- 受理の判定: `state & accept != 0`

このパターンは正規表現で言うところの"ab"にマッチするわけだが、".*a.*b"にマッチするようにすることも簡単にできる
![image](https://gyazo.com/0af6aed29ac322dd24d4577d7490b892/thumb/1000)

- 任意文字での遷移のマスク eps 110
    - 任意文字での遷移の生えている根元の状態にビットが立っている
- 状態の更新: `state = (state & eps) | (state & mask) >> 1`
    - epsマスクで1の立っている状態が一度1になると、その後もずっと1であり続ける
- [[asearch]]の実装では、0x20をこの遷移を意味する文字にしている

あいまい検索
![image](https://gyazo.com/4fc58b867e8bbde5eaafafd6cf7d75da/thumb/1000)
- 1文字誤りを許容するパターンを別の整数で表現する
    - この(1), (2), (3)のそれぞれの遷移について解説しようと思ったが、どうも解説の図と実装に食い違いがあるようなので保留
- (3)の遷移に関して
    - [/masui/曖昧検索asearch](https://scrapbox.io/masui/曖昧検索asearch)の図ではbになっている
    - ![image](https://gyazo.com/d3884cc7d269be9eed5de95a28b261f0/thumb/1000)
    - しかしasearchの実装ではi0をアップデートした後に `i1 |= (i0 >> 1)` しているのでaでの遷移になっている
    - この図における"*"の遷移とasearchの実装は「文字を消費しないイプシロン遷移」ではなくて「任意の1文字での遷移」であるように見える
        - (asearchの実装ではepsilonと言う変数名は使われてはいるが)
    - そのため
        - NFAの図の通りに実装しているなら"ab"は"b"を受理して"a"を受理しない
        - 現状のasearchの実装では"a"を受理して"b"を受理しない
    - 文字を消費しないイプシロン遷移である場合には桂馬とびの遷移(3)がなくても"a"も"b"も受理される
        - ![image](https://gyazo.com/515ce7163d379ad3ffc1c5368a9c456b/thumb/1000)
        - ビット演算でこれを実装するのが楽かどうかは未検討

[https://github.com/masui/asearch-ruby](https://github.com/masui/asearch-ruby)
ruby

```
chars.each { |c|
  mask = @shiftpat[c]
  i3 = (i3 & @epsilon) | ((i3 & mask) >> 1) | (i2 >> 1) | i2
  i2 = (i2 & @epsilon) | ((i2 & mask) >> 1) | (i1 >> 1) | i1
  i1 = (i1 & @epsilon) | ((i1 & mask) >> 1) | (i0 >> 1) | i0
  i0 = (i0 & @epsilon) | ((i0 & mask) >> 1)
  i1 |= (i0 >> 1)
  i2 |= (i1 >> 1)
  i3 |= (i2 >> 1)
}
```


[[レーベンシュタイン距離]]の定義を見ながらどんな遷移があるべきなのかを考える
- ![image](https://gyazo.com/222b0f954e5cbd652709f8af937e4958/thumb/1000)
    - 1文字挿入は、任意の1文字が来たときに、その文字によらず上への遷移が起きれば良いので
        - `i1 |= i0`
    - 1文字置換は、任意の1文字が来たときに、その文字によらず右上への遷移が起きれば良いので
        - `i1 |= (i0 >> 1)`
    - 1文字削除が文字を消費しないイプシロン遷移なのが面倒
        - 「前の文字が来たとき」に、ついでに遷移しておく
        - というわけで文字を消費する遷移が終わった後で `i1 |= (i0 >> 1)`
    - こう考えてみるとasearchの実装の遷移の部分には問題がないことがわかる
    - 問題があるのはここ
ruby

```
def initstate
  [INITPAT, 0, 0, 0]
end
```

        - 最初の文字が来る前のイプシロン遷移でi1〜i3にもビットが立つはずなのに0にしている
    - 図に関しては、イプシロン遷移を使って描くなら斜め遷移がイプシロンも含むということなのだが、使わずに描くならその斜めの遷移が[[Bitapアルゴリズム#5ca57e73aff09e0000f994fd]]の仕組みで2通りの遷移になるので桂馬飛びの線にはa, b両方を描くのが正しそう


その他の話題
- 文字ごとのマスク(shiftpat)は「その文字が来たときに、どの状態が遷移元になるか」を示したものなので、例えば"a"に対応するマスクと"A"に対応するマスクの両方でビットを立てておけばcase-insensitiveなマッチもできる
    - case-insensitiveに限らず、複数種類の1文字で遷移するタイプのものならなんでも。例えば\d。
- 一方「文字ごとのマスク」は、文字ごとに必要なので、日本語文字列に対するマッチに一工夫必要
    - asearchの実装では文字を複数のバイトに分割してバイトごとにマッチしている
        - cons: 日本語の1文字の違いはあいまい検索において2文字の違いになる
            - たまたま2バイトの片方が一致した場合は1文字の違いになる
    - 僕の実装では下位1バイトの情報だけ取って残りを捨てている
:

```
>>> ensure_bytes("こんにちは")
b'S\x93kao'
```

        - ある程度(5文字〜)の長さの日本語文字列の下位1バイトの列がたまたまASCII文字列で意味をなす文字列になる確率は無視できるくらい小さいと考えている
            - cons: asearchの実装みたいに0x20を特殊な意味の文字に使ったりしている場合、日本語文字がたまたまその文字になった時に予期しない挙動になるな

- 速度
    - Scrapboxをクロールして手に入れたページタイトルの集合25743件に対して長さ20のクエリで曖昧検索をして min 29, max 47, med 33 msec だった。
