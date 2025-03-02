---
title: "columnとrowは誤った二項対立"
---

原初の物理世界において[[column]]は「縦に長いもの」であり、当然「横に並ぶ」もの(1)であった。しかし表計算ソフトの普及により「縦に長いもの」を「(中にセルが)縦に並ぶ」もの(2)として解釈する人が生まれ、この2通りの解釈の間の混乱(3)が発生するようになった
![image](https://gyazo.com/d7178eeba09badf38f5eb5ed8debb45b/thumb/1000)
- きっかけが[[表計算ソフト]]かどうかは未検証

[Grid Row - MDN Web Docs Glossary: Definitions of Web-related terms | MDN](https://developer.mozilla.org/en-US/docs/Glossary/Grid_Row)
> Grid Row
>  A grid row is a horizontal track in a CSS grid layout, that is the space between two horizontal grid lines.

[flex-direction - CSS: Cascading Style Sheets | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/flex-direction)
![image](https://gyazo.com/e161d89dc0814a10e5901e9fc926105b/thumb/1000)![image](https://gyazo.com/4159a261f0df16685546b82d2aae2afc/thumb/1000)

[<tr>: The Table Row element - HTML: HyperText Markup Language | MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/tr)
[<colgroup>: The Table Column Group element - HTML: HyperText Markup Language | MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/colgroup)

---
~2024-09-10
> [mizchi](https://x.com/mizchi/status/1833104547453292765) 全然伝わらないので、俺が row と column を覚えられない脳内モデルをビジュアライズしました。
>  なんならこれを見た人全員バグらせてやるぐらいの気持ちがある
>  ![image](https://gyazo.com/a744318a4cc800502754b83e60de9831/thumb/1000)
>  >mizchi: cos と sin はどっちがどっちか覚えられたのに row と column はどっちがどっちか一生覚えられない
> [mizchi](https://x.com/mizchi/status/1833111462216425522) grid-template-areas
>  grid-template-rows
>  grid-template-columns
>  flex-direction: row | column
>
>  この組み合わせを繰り返し記述することで脳が壊れてる

> [nishio](https://x.com/nishio/status/1833104547453292765) 「値渡し？参照渡し？」「[[参照の値渡し]]だよ！」みたいなやつの新しい事例が生まれつつあるw
- [[誤った2]]のどのパターンだろ
    - 僕視点の解釈だと上記の図の1は「rowでもcolumnでもない」で2は「rowのcolumn」
        - 「rowか？columnか？」という思考が混乱の元
        - rowとcolumnが背反だと思ってるのがおかしい
            - じゃあ[[誤った二項対立]]か

> [todesking](https://x.com/todesking/status/1833387101129478600) クソ画像を作っている場合ではない
>  ![image](https://gyazo.com/bf6de72d7d41556845ea9b0bd271a57b/thumb/1000)![image](https://gyazo.com/cb63698084e77578b6e8eaa98462099a/thumb/1000)
- 悪意のある画像だww

> [nishio](https://x.com/nishio/status/1833390030490112206) まあ僕の脳内イメージはこれ
>  ![image](https://gyazo.com/78637371f9242c98ca0d63f3725ef3aa/thumb/1000)
> [nishio](https://x.com/nishio/status/1833391016042500328) 結局、縦に長いものの「中に小さいものが縦に並んでいる」と考えるか、縦に長いものが「横に並んでる」と考えるかは相対的なのでなんの説明にもならないのである

