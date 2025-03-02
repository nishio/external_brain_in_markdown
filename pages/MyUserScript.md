---
title: "MyUserScript"
---

> 個人Projectからimportしているのは個人のカスタマイズという独善性の強い要素のためにこの場でページをageたくないため [/villagepump/kuuote#621e530d4bb2e20000b69a5c](https://scrapbox.io/villagepump/kuuote#621e530d4bb2e20000b69a5c)
- なるほどなと思ったので真似をした
- 最初はUserScriptだけだったけどCSSも付け加わって、更にアイコンもセットにしたので名前が適切でない感
- リネームしても他のプロジェクトからのリンクが壊れないかな？？

「自分のページ」に顔アイコンをつけてたころ、コードを編集するたびにデカデカと顔の載ったカードが上がってくることに関してあんまりよく思ってなかった
- その違和感を言語化できてなかったけど「見て欲しいわけではないものが上がってくること」に対する心理的抵抗だったわけだな
- 顔アイコンを変えたら少し快適になった
- こちらのプロジェクトに関しては、ピン留めした上でCSSで消した
    - [[faviconページをCSSで消す]]

for new mypage

```
[https://gyazo.com/33506f42d0d01848cfb88ad9b785ab31]
[/nishio]

code:style.css
  @import "https://scrapbox.io/api/code/nishio/MyUserScript/style.css";
code:script.js
  import '/api/code/nishio/MyUserScript/script.js'
#member
```


---

[[リンクをたどって到達できるページを全部まとめるJS]]
×script.js

```javascript
import '/api/code/nishio/リンクをたどって到達できるページを全部まとめるJS/script.js'
```


[[PomodoroScrapbox]]
×script.js

```javascript
import '/api/code/nishio/PomodoroScrapbox/script.js'
```


[[open with porter]]
×script.js

```javascript
import '/api/code/nishio/open_with_porter/script.js'
```


[[ToMyProj]]
×script.js

```javascript
import('/api/code/nishio/ToMyProj/script.js');
```


[/takker/選択範囲をMarkdown記法に変換してclip boardにcopyするPopupMenu](https://scrapbox.io/takker/選択範囲をMarkdown記法に変換してclip boardにcopyするPopupMenu)
×script.js_disable

```
import("/api/code/takker/%E9%81%B8%E6%8A%9E%E7%AF%84%E5%9B%B2%E3%82%92Markdown%E8%A8%98%E6%B3%95%E3%81%AB%E5%A4%89%E6%8F%9B%E3%81%97%E3%81%A6clip_board%E3%81%ABcopy%E3%81%99%E3%82%8BPopupMenu/script.js");
```


[[AskChatGPT]]
×script_disabled.js

```javascript
import('/api/code/nishio/AskChatGPT/script.js');
```


[[ChatGPTToScrapbox]]
×script.js

```javascript
import('/api/code/nishio/ChatGPTToScrapbox/script.js');
```


2018-09-19 日時のフォーマットを←にする
script.js

```javascript
scrapbox.TimeStamp.removeAllFormats()
scrapbox.TimeStamp.addFormat("YYYY-MM-DD")
```




CSS

imports
[[インデント表示]]
style.css_disable

```
@import "https://scrapbox.io/api/code/nishio/%E3%82%A4%E3%83%B3%E3%83%87%E3%83%B3%E3%83%88%E8%A1%A8%E7%A4%BA/style.css";
```


[/noratetsu/●「行番号を表示する」改良版](https://scrapbox.io/noratetsu/●「行番号を表示する」改良版)
style.css_disable

```
/* 行番号を表示 -- ウィンドウ幅768px以上で適用 */
@media screen and (min-width: 768px) {
  .editor .lines { counter-reset: line }
  
  /* タイトルから数えるときは :not(.line-title) を消してね */
  .editor .line:not(.line-title) { counter-increment: line }
  
  /* タイトルから数えるときは :not(.line-title) を消してね */
  .app:not(.presentation) .editor .line:not(.line-title)::before { 
    content: counter(line); 
    position: absolute; display: inline-block; left: -110px; z-index: 10; 
    min-width: 50px; text-align: right; vertical-align: middle;
    
    /* 行番号のフォントとか色とかの指定はここ */
    font-family: monospace; color: grey }
  
  /* カーソル行の行番号を濃く表示する */
  .editor .line:not(.line-title)::before { opacity: .5 }
  .editor .line.cursor-line:not(.line-title)::before { opacity: 1; font-weight: bolder } }
```

