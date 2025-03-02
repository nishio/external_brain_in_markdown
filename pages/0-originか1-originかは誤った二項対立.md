
[[0-origin]]か[[1-origin]]かは[[誤った二項対立]]

A: Luaは配列の添字が1から始まるんですよね(1-origin)
B: BASICもそうですね
C: いやBASICは0-originでしょう
D: それは両方あって、後に切り替えられる仕様が標準になったんですよ

[Minimal BASIC - Wikipedia](https://en.wikipedia.org/wiki/Minimal_BASIC)
> Minimal BASIC is a dialect of the BASIC programming language developed as an international standard. The effort started at ANSI in January 1974, and was joined in September by a parallel group at ECMA.
> ...
>  The lower bound for arrays is typically 0, but using OPTION BASE 1 can change the index to 1.
`OPTION BASE 1`で切り替えられる

VBAなどでもちゃんと実装されている
- [Option Base ステートメント (VBA) | Microsoft Learn](https://learn.microsoft.com/ja-jp/office/vba/language/reference/user-interface-help/option-base-statement)
