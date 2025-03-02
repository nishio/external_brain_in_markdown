
[[Unity]]
- `$"FPS: {frameCount / timeDelta : F1}"` でいけるはずだったんだけど、Unity側が「その機能はC#4.0では使えない」って怒る
- 仕方がないのでtoStringで変換した
    - [$ - 文字列補間 (C# リファレンス) | Microsoft Docs](https://docs.microsoft.com/ja-jp/dotnet/csharp/language-reference/tokens/interpolated)
    - [標準の数値書式指定文字列 | Microsoft Docs](https://docs.microsoft.com/ja-jp/dotnet/standard/base-types/standard-numeric-format-strings#FFormatString)

JS
- [Number.prototype.toFixed() - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/toFixed)