
see もっといいやつ→[[Scrapbox振り返り機能]]

script.js

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
  title: 'Scrapbox SRS',
  image: 'https://gyazo.com/11140c8b35b407c5d490a94ec6f2528f/raw',
  onClick: () => {
    scrapbox.PageMenu('Scrapbox SRS').addItem({ title: 'Please wait...', image: null, onClick: () => null })
    get_data();
    scrapbox.PageMenu('Scrapbox Sort').removeAllItems()
  }
})
```

