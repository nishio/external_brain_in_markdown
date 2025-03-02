
状況はMac。
PowerPoint上でハイパーリンクの形でリンク集が作られている。
PowerPoint外にその情報を転記したいが、1つ1つ選んでURLの情報をコピペするのは面倒。
どうするのが楽だと思うか？と聞かれたので少し考えてみた結果、こうなった

- PowerPoint上でリストをコピー
- Macのテキストエディタに貼り付ける
    - リッチテキストエディタなのでハイパーリンクのまま貼り付けられる
- テキストエディタはHTML形式で保存できるので、やる
- 保存されたHTMLはこんな感じ
html

```html
<p class="p1"><span class="s1"><a href="https://www.j-focus.or.jp/archives/001/201307/5715be09b5800.pdf">【ナノテク・材料】環境負荷低減高性能タイヤの開発</a></span></p>
<p class="p1"><span class="s1"><a href="https://www.j-focus.or.jp/archives/001/201307/5715be09ba60c.pdf">【ナノテク・材料】排気ガス浄化用触媒シミュレーション</a></span></p>
<p class="p1"><span class="s1"><a href="https://www.j-focus.or.jp/archives/001/201307/5715be09bc047.pdf">【ナノテク・材料】鉛フリー釣り用オモリの開発</a></span></p>
```

- HTMLが使えるならそれでも良いし、さらに変換したいなら正規表現などを使って置換する

備考
- PowerPointから直接HTML形式で出せるのでは？って思ったが見つけられなかった
- 昔ExcelがHTMLを読み書きできることを利用したハックをやったなぁと思い出した
