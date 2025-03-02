---
title: "ToMyProj"
---

元の文章を破壊しないで抜き出すユーザスクリプト
- 元々は「他のプロジェクトに書かれてる内容を自分のプロジェクトにコピーして整理するため」に作られた
    - なので出典リンクとアイコンはプロジェクト名をつける仕様になってる
- 2022-11-25 しばらく使ってて、同一プロジェクト内でも有用だと思った
    - 今の公式の「New Page」の機能は、元ページの内容を変更する
    - なのでその変更に悪影響がないかを心配しながら使うことになり心理的ハードルが高い
    - 一旦「元ページは変更しないで」抜き出して、整理してから、元ページの記述を消すのか修正するのを考える方が苦痛が少ないのではないか

2022-01-19
他のプロジェクトの記述を自分のプロジェクトに複製するときに
- アイコンを元プロジェクトへの参照にして壊れないようにする
- 出典リンクを挿入する

こうなる
- [[井戸端2022-01-17]]　タイトルはいじった
    - プロジェクト内リンクを元プロジェクトへのリンクにすべきかどうか…
        - こっちのプロジェクトの何ともつながらなくなるよな
        - [[しないべき]]
            - 同名のページがこちらのプロジェクトにもあるならそれはつながるべき
            - 「つながらない=このプロジェクトにない」もまた情報量
                - [[空白の存在に気づく]]
            - 作るコストをかけてでも必要だと思うなら作ればいいし、それほどでもないなら放置で良い
2022-02-01
- 井戸端から他のプロジェクトのアイコンを参照してるところが壊れる
- タイトルが「Re:」だが、日記のページはタイトルを事後的に修正しているので、間違えて重複させてしまった
    - まあでも、それ以外のページでもタイトル修正はするか
    - リンクが繋がるのでまあ気付くことはできる
- /nishioへのリンクはプロジェクト内リンクに機械的に戻しても良いかも
2022-03-26
- ページを作りたいとは限らない
    - たとえば既存のページに、そのページに対する他のプロジェクトでの言及を加筆するとき
    - なのでクリップボードに入れて、それからページを作成するかどうか聞くようにした

ToMyProj
script.js

```javascript
scrapbox.PopupMenu.addButton({
  title: 'ToMyProj',
  onClick: text => {
    const dst = 'nishio'
    const src = scrapbox.Project.name
    const new_text = text.replace(/\[([^\]\/]+).icon\]/gm, `[/${src}/$1.icon]`)

    const lines = new_text.split(/[\r\n]/g)

    const title = scrapbox.Page.title
    lines.unshift(`from [/${src}/${title}]`)

	const title_url = encodeURIComponent(title)
    const body = lines.join('\n')
    navigator.clipboard.writeText(body).then(()=>{
      if (window.confirm("copied. create page?")) {
        const body_enc = encodeURIComponent(body)
        window.open(`https://scrapbox.io/${dst}/Re:${title_url}?body=${body_enc}`)
      }
    })
  },
})
```

