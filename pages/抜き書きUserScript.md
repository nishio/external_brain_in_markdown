---
title: "抜き書きUserScript"
---

2021-08-04
- 言及されて思い出した
    - [https://twitter.com/dedededalus/status/1422578181870014467?s=21](https://twitter.com/dedededalus/status/1422578181870014467?s=21)
- [[ScrapboxSRS]]
- SRSはSpaced Repetition Systemで、徐々に伸びる間隔で読み返すことを支援するシステムです。長期間更新してないページがたまに浮上して見返す機会を作るという感じです。
- 使い続けてない
- 今振り返って考えると「昔のページがたまに浮上して見返す機会を作る」って目的ではあんまり短期のリンクを出す必要がなかったのでは
    - 「[[n年前のこの日]]」で良い説
- 作り直すなら
    - 「100日前」「1年前」「数年前」の3つでそれぞれ数件ずつ表示
    - 金曜の会議の合間で改良版を作ろうかな

---

2018-06-22
- ページの1部分を新規ページに引用形式で切り出す
- 元ページは編集しない
- 新規ページから元ページへは行パーマリンクを貼る
ってのを作りたい

元ページは編集されない？
- 編集されても良い？

これがあると何ができるか
[[ScrapboxでIncremental Reading]]

行パーマリンクの作り方がわからなかったが [[window.scrapbox.Page]] のlinesにパーマリンクとテキストがセットで入っている

今のNew Page機能ではダメなのか？なぜダメなのか？
- [[人間は削除に抵抗を感じる]]
- 元の文章が残っているという安心感があれば、削除、編集ができる
- だから元の文章は手付かずでなければならない

[[Scrapboxと長文]]


script.js

```javascript
function clip(text){
debugger;
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
      window.open(`${projectRoot}/Re:${currentPageTitle}?body=${body}`)
      return text
}
scrapbox.PopupMenu.addButton({title: 'Clip', onClick: clip})

```



js

```javascript
  scrapbox.PopupMenu.addButton({
    title: 'NewPage2',
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


js

```javascript
const sortMode = 'log' // 間隔反復法
let visibleRankNum = 100; // log以外では無視される
const day = 60 * 60 * 24 * 1000
const year = day * 365
let projectPages;

function get_data(){
  let xhr = new XMLHttpRequest()
  xhr.open('GET', `/api/pages/${scrapbox.Project.name}?limit=10000`)
  xhr.onload = (e) => {
    projectPages = JSON.parse(xhr.responseText).pages
    sort_pages()
    update_list()
  }
  xhr.send(null)
}

function sort_pages(){
  const now = Date.now()
  projectPages.forEach((page, index, pages) => {
    let diff = now - page['updated'] * 1000
    if(diff > 10 * day){
      page['score'] = (Math.log(diff / (10 * day)) / Math.log(2)) % 1
      page['ago'] = Math.floor(diff / day)
    }
  })
  projectPages = projectPages.filter(page => (page['score'] != null))
  projectPages.sort((a, b) => (a['score'] - b['score']))
}

function create_page(title, lines){
  const projectRoot = (() => {
    const tmp = location.href.split('/')
    tmp.pop()
    return tmp.join('/')
  })()
  const body = encodeURIComponent(lines.join('\n'))
  window.open(`${projectRoot}/${title}?body=${body}`)
}

function update_list(){
  scrapbox.PageMenu('Scrapbox Sort').removeAllItems()
  let page_lists = [];
  for (let i = 0; i < visibleRankNum; i++) {
    let page = projectPages[i]
    if(page == null) break;
    page_lists.push(`${strftime(new Date(page.updated * 1000))}(${page['ago']}) [${page['title']}]`)
  }
  create_page("SRS" + new Date().toISOString().slice(0, 19), page_lists)
}

function pad(number) {
  if (number < 10) {
    return '0' + number;
  }
  return number;
}

function strftime(d){
  return (
    d.getUTCFullYear() +
    '-' + pad(d.getUTCMonth() + 1) +
    '-' + pad(d.getUTCDate())
  )
}
scrapbox.PageMenu.addMenu({
  title: 'Scrapbox SRS2',
  image: 'https://gyazo.com/11140c8b35b407c5d490a94ec6f2528f/raw',
  onClick: () => {
    scrapbox.PageMenu('Scrapbox SRS').addItem({ title: 'Please wait...', image: null, onClick: () => null })
    get_data();
    scrapbox.PageMenu('Scrapbox Sort').removeAllItems()
  }
})
```

