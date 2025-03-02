
Scrapboxのページで実行するとタイトルに鍵をつけたページをprivateプロジェクトに作るUserScript。地球マークが元のページへのリンクになっている。
![image](https://gyazo.com/ef344a8d007bee6b11d949c2278d0d88/thumb/1000)

script.js

```javascript
const privateProject = "..."
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

