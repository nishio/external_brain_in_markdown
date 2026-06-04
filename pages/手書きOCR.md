---
title: "手書きOCR"
---

2026-05-20
> [gyakuse](https://x.com/gyakuse/status/2056969256483553760) [[Gemini 3.5 Flash]], ﾒﾁｬ汚い手書き文字OCR界隈としては最強性能です。新規検証しました。
>  [https://nyosegawa.com/posts/japanese-handwriting-ocr-comparison/](https://nyosegawa.com/posts/japanese-handwriting-ocr-comparison/)

汚い手書きのOCR能力、ついに僕の手書きメモが活用可能になる時が来るか？
![image](https://gyazo.com/7a160bf95ac5f997d624867298a82e12/thumb/1000)
ocr

```
210 2013-03-30 文具をケチるのは合理的でないと論破されたのでモレスキンフォリオ
スクエアードを買って見た.

トリフール [?] 10^35
梅花碁 3^19x19 ≒ 10^172 そこ 573

バインダーにはさまっていた紙をレビューした. 半分くらいすてて残りをクリアファイルに入れてはさんだ.
「やりたいこと」組をレビューしてこの冊に書きうつす

ATMEGA168をArduinoとして使うには AVRライタを買ってブートローダを書き込む必要
がある. 1000円台. MacにFTDIドライバを入れる必要もある. Arduino開発環境でポートに
USB-Serialが表示されずカキコミに失敗する.

15ピン VGA
B G R
● = GND
VSYNC GND(for 800x600)?
HSYNC
I2C Clock I2C Data 画面サイズの情報
```


打ち消し線とか図解とか、汚い数式はミスっているが「なんの話を書いているか」を読み取る上では問題ないクオリティ
6冊OCRして何円か見積もったら1500円くらいとのこと
- これはOCRしてLLM Wikiにするか？！

なおこの画像をGyazoにあげたことでGyazo側でもOCRが走る
gyazo_ocr

```
210 2013-03-30 文具をケチののは合理的でないと論破されたのでモレスキンフォリオ
スクエアードを買って見た。
トリコロール
10
35
19×4
梅花 39 =10722
573
バインダにはさまっていた紙をレビューした。半分くらいすてて、のこりをクリアファイルに入れてはさんだ。
「やりたいこと」紙をレビューしてここに書きうつす
ATMEGA168Andlineとして使うには AVRライタを買ってブートローダを書き込む必要
がある。1000円台。MacにFTDエドライバを入れる必要もある、Arduino用環境でポートに
CSB-Serialが表示されずカキコミに失敗する。
15ピン VGA
BGR
250
• 0 °
११११
VSYNC)
HSYNC
Be Clock
.
●=GND
GND for 800x600)?
12C Data
画面サイズの情報
```


文脈理解力の差を感じる
- > ATMEGA168をArduinoとして使うには
- > ATMEGA168Andlineとして使うには
- 「ATMEGA168の話をしてるんだからArduinoだろ」とGeminiは賢く推測してそう
    - こういう専門用語的なキーワードが正しく読まれてることが、後で検索とかするときの効率に効いてきそう

[[OCR]]

