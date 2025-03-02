---
title: "CopyToClipboard"
---

「何かをクリップボードにコピーする」という作業を手軽にするブックマークレットを作る話

今までのいきさつ
- [/yujif/今見ているページをScrapboxのリンク形式でコピーできるブックマークレット](https://scrapbox.io/yujif/今見ているページをScrapboxのリンク形式でコピーできるブックマークレット)
- [/shiology/05107-180420 今見ているページのScrapboxリンクをワンクリックでコピーできるようになった](https://scrapbox.io/shiology/05107-180420 今見ているページのScrapboxリンクをワンクリックでコピーできるようになった)
- [/shiology/05148-180531 flickrのScrapboxリンクを取得するブックマークレットを書きました](https://scrapbox.io/shiology/05148-180531 flickrのScrapboxリンクを取得するブックマークレットを書きました)

現時点のまとめ
- 最新のChromeでブックマークレットからexecCommandを起動した場合返り値がfalseでコピーされない
- 同じコードをdevtoolから実行すると返り値がtrueでコピーされる
- これは`outside a user-generated event handler`的な問題に思えるが、何か回避方法はあるのか？

-----
実装1
javascript

```javascript
function copy_impl1(target){
	// コピー機能の実装1: 目的の文字列が入ったinputエレメントを作成し、それを選択してコピーコマンドを実行
 	// MacのChrome、Safariでは動くがiOSのSafariではダメらしい
	const e=document.createElement('input');
 	e.value=target;
  	document.querySelector('body').append(e);
    e.select();
    document.execCommand('copy');
    e.remove();
}) 
```


実装2
js

```javascript
function copy_impl2(target){
	// コピー機能の実装2: 目的の文字列が入ったtextareaエレメントを作成し、
 	// 0から999999文字目まで選択してコピーコマンドを実行
 	// iOS, MacともSafariで動作確認済み
	var a = document.createElement("textarea");
	a.textContent = target;
    var b = document.getElementsByTagName("body")[0];
    b.appendChild(a);
    a.contentEditable = true;
    a.readOnly = false;
    a.setSelectionRange(0, 999999);
    document.execCommand("copy");
    b.removeChild(a)
}
```


- 2つを比較してみると、大きな違いはtextareaを使うことと、contentEditableをtrueにすること
- querySelectorはiOSのSafariでもサポートされてる [https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector)

でもまあ深追いはしないで今回は単に両方呼んでしまおう
- うまく動かなかった
- 第3案
- [http://yuw27b.hatenablog.com/entry/2017/02/19/230000](http://yuw27b.hatenablog.com/entry/2017/02/19/230000)
- 選択の方法に違いがあるな

js

```javascript
function copy_impl3(target){
	// コピー機能の実装3: 目的の文字列が入ったpエレメントを作成しそれを選択してコピーコマンドを実行、
	var a = document.createElement("p");
    var b = document.querySelector("body")
    b.append(a);
	var range = document.createRange();
 	range.selectNode(a);
 	window.getSelection().removeAllRanges();
 	window.getSelection().addRange(range);
 	document.execCommand('copy');
}
```

この方法で、pエレメントが追加されてそれが選択されるところまでは確認されたが、コピーされてない。

Chrome
- impl1ではe.selectでinputが選択されていることを確認した
- しかしコピーされていない
- その後devtoolからdocument.execCommand('copy')を実行したらコピーされてる
- この時の返り値はtrue
- ブックマークレットからの実行ではfalse

さらに別解
js

```javascript
function copy_impl4(target){
	let copyListener = event => {
 		document.removeEventListener("copy", copyListener, true);
  	event.preventDefault();
  	let clipboardData = event.clipboardData;
 		clipboardData.clearData();
 		clipboardData.setData("text/plain", target);
	};
	document.addEventListener("copy", copyListener, true);
	document.execCommand("copy");
	document.removeEventListener("copy", copyListener);
}
```

この場合もブックマークレットからの起動では動かず、execCommandはfalse、devtoolで実行するとちゃんとコピーされる

というわけで全部入りのコードは下記
main.js

```javascript
function copy_impl1(target){
	// コピー機能の実装1: 目的の文字列が入ったinputエレメントを作成し、それを選択してコピーコマンドを実行
 	// MacのChrome、Safariでは動くがiOSのSafariではダメらしい
	const e=document.createElement('input');
 	e.value=target;
  	document.querySelector('body').append(e);
  	console.log(e)
    e.select();
    console.log(document.execCommand('copy'));
    //e.remove();
}
function copy_impl2(target){
	// コピー機能の実装2: 目的の文字列が入ったtextareaエレメントを作成し、
 	// 0から999999文字目まで選択してコピーコマンドを実行
 	// iOS, MacともSafariで動作確認済み
	var a = document.createElement("textarea");
	a.textContent = target;
    var b = document.getElementsByTagName("body")[0];
    b.appendChild(a);
    a.contentEditable = true;
    a.readOnly = false;
    a.setSelectionRange(0, 999999);
    console.log(window.getSelection())
    document.execCommand("copy");
    //b.removeChild(a)
}
function copy_impl3(target){
	// コピー機能の実装3: 目的の文字列が入ったpエレメントを作成しそれを選択してコピーコマンドを実行、
	var a = document.createElement("p");
 	a.textContent = target;
    var b = document.querySelector("body")
    b.append(a);
    console.log(a)
	var range = document.createRange();
 	range.selectNode(a);
    console.log(range)
 	window.getSelection().removeAllRanges();
 	window.getSelection().addRange(range);
 	document.execCommand('copy');
    console.log(window.getSelection())
}
function copy_impl4(target){
	let copyListener = event => {
 		document.removeEventListener("copy", copyListener, true);
  	event.preventDefault();
  	let clipboardData = event.clipboardData;
 		clipboardData.clearData();
 		clipboardData.setData("text/plain", target);
	};
	document.addEventListener("copy", copyListener, true);
	console.log(document.execCommand("copy"));
	document.removeEventListener("copy", copyListener);
}
function main(){
	var target = `[${document.title.replace(/\s*[\[\]]\s*/g,' ')} ${location.href}]`;
 	//copy_impl1(target);
  	//copy_impl2(target);
    //copy_impl3(target);
    copy_impl4(target)
    console.log("ok")
}
main();
```


これが`https://scrapbox.io/api/code/nishio/CopyToClipboard/main.js`でアクセスできるので

javascript: var url="[https://scrapbox.io/api/code/nishio/CopyToClipboard/main.js";var](https://scrapbox.io/api/code/nishio/CopyToClipboard/main.js";var) elm=document.createElement('script');elm.setAttribute('src', url);document.body.appendChild(elm);

a
a
