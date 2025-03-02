---
title: "nishio"
---

これはScrapboxの仕様上、あるとベターな[[自分のページ]]です。

![image](https://gyazo.com/03051565f03a70a83b182fda5965e187/thumb/1000)
- こうやって個人ページを作っておくとCtrl+iでアイコンが出るようになる
- 画像の貼られたページを最初にピン止めしておくことでそれがFaviconになり、ブラウザのタブなどでわかりやすい。
- [[自己紹介]]
- [西尾泰和](http://www.nhiro.org/)

![image](https://gyazo.com/c078c5aa55ddbddd85530c5136b163e8/thumb/1000)



-----以下個人的なカスタマイズのためのユーザースクリプトなど-----

[[MyUserScript]]
style.css

```
 @import "https://scrapbox.io/api/code/nishio/MyUserScript/style.css";
```

script.js

```javascript
 import '/api/code/nishio/MyUserScript/script.js'
```

---

[[pin-diary-X]]
script.js

```javascript
import "/api/code/nishio/pin-diary-X/min.js"
```



[[最近開いてないページ]]
disabled_script.js.disabled

```
import "/api/code/nishio/最近開いてないページ/script.js"
```


[[add watchlist]]
script.js.disabled

```
import '/api/code/nishio/add_watchlist/script.js'
```


[[open with mem]]
script.js

```javascript
import '/api/code/nishio/open_with_mem/script.js'
```


[[open with quartz]]
script.js

```javascript
import '/api/code/nishio/open_with_quartz/script.js'
```


[[open with porter]] Moved To MyUserScript
script.js.disabled

```
import '/api/code/nishio/open_with_porter/script.js'
```



[[ScrapBubble]] [/takker/takker99/ScrapBubble](https://scrapbox.io/takker/takker99/ScrapBubble)
script.js.disabled

```
import { mount } from "../ScrapBubble-min/app.js";

mount({
  whiteList: ["nishio"]
});
```



[[ScrapboxでCtrl+EnterしてKeichoに質問させる]]
script.js.disabled

```
import('/api/code/nishio/ScrapboxでCtrl+EnterしてKeichoに質問させる/script.js');
```


## 全角半角変換などをする「format」メニュ
 (from [/shiology](https://scrapbox.io/shiology))
1. 箇条書きの先頭を全てTabに置き換える
2. 文中の全角・半角空白を取り除く
3. 文字化けを修正する (今回は `での` を `での` に直す)
4. 全角英数字を半角英数字に置き換える
5. 全角括弧を半角括弧に置き換える
6. 括弧で囲まれた前後に空白を入れる
7. コードブロック記法の前後に空白を入れる
script.js.disabled

```
scrapbox.PopupMenu.addButton({
    title: 'format',
    onClick: text => text.split('\n').map(function(line) {
        return line.replace(/^\s*/g, s => s.replace(/\s/g, '\t'))
//            .replace(/[ 　]/g, '')
            .replace(/[ぁ-ん|ァ-ヴ]゙/g, s => String.fromCharCode(s.charCodeAt(0) + 1))
            .replace(/[Ａ-Ｚａ-ｚ０-９]/g, s => String.fromCharCode(s.charCodeAt(0) - 0xFEE0))
            .replace('（', '(')
            .replace('）', ')')
            .replace(/\S\(/g, s => s.charAt(0) + ` (`)
            .replace(/\)\S/g, s => ') ' + s.charAt(1))
            .replace(/\S`.*`/g, s => s.charAt(0) + ' ' + s.slice(1))
            .replace(/`.*`\S/g, s => s.slice(0, -1) + ' ' + s.slice(-1))
    }).join('\n')
})
```


[[Scrapbox横断検索]]
script.js.disabled

```
var pagename = document.location.pathname.split("/").pop();
if(pagename == "cross_search"){
	console.log(pagename);
	var query = document.location.search.substr(1);
	var page = document.getElementsByClassName("page")[0];
	page.innerHTML = "<iframe width='50%' height='2000px' src='https://scrapbox.io/rashitamemo/search/page?q=" + query + 
"'></iframe><iframe width='50%' height='2000px' src='https://scrapbox.io/nishio/search/page?q=" + query + "'></iframe>" + page.innerHTML;
}

```



[/masui/検索してみつからなければ新規作成](https://scrapbox.io/masui/検索してみつからなければ新規作成)
[[改行キーで新規ページ作成]]
disabled_script.js.disabled

```
$('body').on('keydown',function(e){ // Enterキーで新規ページ作成
   if(e.target.tagName != "TEXTAREA" && e.target.tagName != "INPUT"){
      if(e.key == 'Enter'){
         var project = location.href.split('/')[3];
         location.href = `/${project}/new`;
      }
   }
});
$('.btn.btn-default').on('click',function(){
   var s = $('.form-control').val();
   if(s == ''){
      var project = location.href.split('/')[3];
      location.href = `/${project}/new`;
   }
});
```


## タイムタギング
年のタグ、月日のタグ、年月のタグを作る。「何年ごろ何やってたかな」もできるし「何年の何月ごろ」と狭めることもできる。月日のタグは「[[過去のこの日]]」に使う。
script.js.disabled

```
 scrapbox.PopupMenu.addButton({
   title: "TimeTag",
   onClick: (text) => {
   	 var m = text.match(/((\d\d)?(\d\d))-?(\d\d)-?(\d\d)/);
     var year = "20" + m[3];
     var month = m[4];
     var day = m[5];
     return `${year}-${month}-${day} #${year} #${month}-${day} #${year}-${month}`;
   }
 })
```


2018-09-19 日時のフォーマットを←にする
Moved To MyUserScript
script.js.disabled

```
scrapbox.TimeStamp.removeAllFormats()
scrapbox.TimeStamp.addFormat("YYYY-MM-DD")
```


2018-06-22
script.js.disabled

```
import '/api/code/nishio/抜き書きUserScript/script.js'
```

see [[抜き書きUserScript]]

2018-06-12
小さくする
script.js.disabled

```
 var elm=document.createElement('span');
 elm.append("ZoomOut")
 elm.onclick = ()=>{
   		document.getElementsByClassName("page-list")[0].setAttribute('style', 'zoom: 0.5')
     	document.getElementsByTagName('body')[0].webkitRequestFullscreen()
 }
 document.getElementsByClassName("search-form")[0].parentElement.append(elm) 
```




2018-05-25
- [/customize/「過去のこの日」機能](https://scrapbox.io/customize/「過去のこの日」機能)
- [[Scrapbox振り返り機能]]
script.js.disabled

```
import '/api/code/nishio/Scrapbox振り返り機能/script.js'
```


## 音声入力
2018-04-15
[/shokai/音声入力Menu](https://scrapbox.io/shokai/音声入力Menu)
script.js.disabled

```
import '/api/code/shokai/音声入力Menu/script.js'
```


塩澤先生のプロジェクトから

## tweetメニュ
script.js.disabled

```
scrapbox.PageMenu.addItem({
  title: 'Tweet',
  image: 'https://twitter.com/favicon.ico',
  onClick: () => window.open(`https://twitter.com/intent/tweet?url=${encodeURIComponent(location.href)}&text=${encodeURIComponent(document.title)}`)
})
```


## 文字数カウントメニュ
script.js.disabled

```
 scrapbox.PageMenu.addItem({
   title: () => {
     if (!scrapbox.Page.lines) return
     const chars = scrapbox.Page.lines.map(line => line.text.length).reduce((a,b) => a + b)
     const words = scrapbox.Page.lines.map(line => line.text.split(/\s+/).length).reduce((a,b) => a + b)
     return `${chars}文字 ${words}単語 ${scrapbox.Page.lines.length}行`
   },
   onClick: () => null
 })
```


## 文字数カウンタ
[[見える文字数カウンター]]
style.css_disabled

```
@import "/api/code/nishio/見える文字数カウンター/style.css";
```

script.js_disabled

```
import "/api/code/nishio/見える文字数カウンター/script.js";
```



## 選択文字列をプロジェクト内で検索ポップアップ
script.js.disabled

```
// 選択された文字列をScrapboxプロジェクト内で検索する
// Scapbox検索ボックスを使ったときと同じ結果ページを開く
scrapbox.PopupMenu.addButton({
    title: 'SB内検索',
    onClick: function (text) {
    	var projectName = 'shio';
     	window.open('https://scrapbox.io/'+ projectName +'/search/page?q=' + text);
    }
});
```



---
ページの1部分を新規ページに切り出す
disabled_script.js.diabled

```
scrapbox.PopupMenu.addButton({
  title: 'NewPage',
  onClick: text => {
    const lines = text.split(/[\r\n]/g)
    const title = lines[0]
      .trim()
      .replace(/\[[^\]]+.icon\]/gm, '')
      .replace(/[\[\]]/g, '')
    const projectRoot = (() => {
      const tmp = location.href.split('/')
      tmp.pop()
      return tmp.join('/')
    })()
    const currentPageTitle = decodeURIComponent(location.href.split(/\//g).pop())
    lines.unshift(`from [${currentPageTitle}]`)
    const body = encodeURIComponent(lines.join('\n'))
    window.open(`${projectRoot}/${title}?body=${body}`)
    return `[${title}]`
  }
})
```


2021-05-06
[[to🔒]]
script.js.disabled

```
const privateProject = "znishio"
scrapbox.PageMenu.addItem({
  title: 'to🔒',
  onClick: () => {
	const title = document.location.pathname.split("/")[2];
	window.open(`https://scrapbox.io/${privateProject}/🔒${title}`, "_blank")
  }
})
scrapbox.PageMenu.addItem({
  title: 'make🔒',
  onClick: () => {
	const title = document.location.pathname.split("/")[2];
	const body = `[https://scrapbox.io/nishio/${title} 🌏] [${title}]`
	window.open(`https://scrapbox.io/${privateProject}/🔒${title}?body=${body}`, "_blank")
  }
})
```


[[paddingふやす]]
style.css.disabled

```
a.mobile-search-toggle {
    padding: 1em;
}
.toggle-button.closed {
    padding-right: 1em;
}
.toggle-button.open {
    padding-right: 1em;
}
```

