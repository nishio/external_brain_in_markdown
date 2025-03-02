---
title: "Scrapbox振り返り機能"
---

2021-08-06 ワンクリックで下記のようなページが生成される
![image](https://gyazo.com/5a863b3913690508695b5d0b210c2619/thumb/1000)
想定してる使い方
- 気が向いた時にメニューをクリック
- 生成されたページを見る
    - リンク先をたどってみたくなったらたどる
        - リンク先を書き換えたくなったら書き換える
        - 書き換えないけどコメントつけたかったらこの振り返りページに「昔はこんなことを書いてたけど〜」みたいにコメントを書く
            - 複数のリンク先をみて、関係を見出したりするかもしれない
            - 書いてからさらにタイトルをつけて独立したページにしたくなったらそうする
    - 見てアクションする気にならなかったものはリンクを消す
        - たぶんこれが大事
        - これをやらないと意味のないリンクが増えてScrapboxがゴミ屋敷になる
    - リンク先のページを書き換えたものも、リンクを消したらいいと思う
        - 「この日の振り返りで見返した」って情報にあんまり意味がないから
    - この振り返りページは振り返りによって生まれた情報の一時的な居場所として使って、最終的には散り散りになってページがなくなるのが理想
        - 良い居場所が見つからなかった場合に仕方なくここに残る、[[思考の結節点]]みたいに。

以前のバージョン[[ScrapboxSRS]]との比較
- 以前はリンクをたくさん出しすぎたと思う
    - 全部見るのが負担になってしまう
    - 他にも不必要に情報量が多かった
    - 3年ぶりに見たら「いや、多すぎだろ」となった
- スコアの意味の解釈が難しくて良くない
    - というわけで「100日前」「1年前」「n年前」の3つにした
        - 「n年前」は1年前以外で1年の倍数に近いもの
- 各セクション3つにした
    - 3×3の9個くらいがちょうどいいんじゃない？という意図

使ってみた
- [[「2021-08-05振り返り」の振り返り]]

[/takker/Scrapbox振り返り機能#610c18a51280f00000ed3fc3](https://scrapbox.io/takker/Scrapbox振り返り機能#610c18a51280f00000ed3fc3)
- > 外部projectリンク記法にして、リンクが残っても関連ページリストに出てこないようにした
    - なるほど

2021-08-06
script.js

```javascript
const LINE_PER_SECTION = 3;
const day = 60 * 60 * 24 * 1000;
const year = day * 365;

const project_name = scrapbox.Project.name;
const project_root = `https://scrapbox.io/${project_name}`;
const menu_title = "振り返り";
const make_title = () => `${strftime(new Date())}${menu_title}`;

// score: 0 is best
const sections = [
  {
    title: "100日前",
    score: (diff) => Math.abs(diff - 100 * day),
  },
  {
    title: "1年前",
    score: (diff) => Math.abs(diff - year),
  },
  {
    title: "n年前",
    score: (diff) => {
      // excludes 1年前
      if (diff < year * 1.5) {
        return year;
      }
      const mod = diff % year;
      return Math.min(mod, year - mod);
    },
  },
];

const main = () => {
  // calc scores
  const now = Date.now();
  const scored_pages = [];
  scrapbox.Project.pages.forEach((page) => {
    const updated = page.updated;
    if (updated === 0) return;
    const diff = now - updated * 1000;
    const p = { ...page };
    sections.forEach((sction) => {
      p[sction.title] = sction.score(diff);
    });
    scored_pages.push(p);
  });

  // generate page contents
  const lines = [];
  sections.forEach((section) => {
    scored_pages.sort((a, b) => a[section.title] - b[section.title]);
    lines.push(section.title);
    scored_pages.slice(0, LINE_PER_SECTION).forEach((page) => {
      const title = page["title"];
      const date = strftime(new Date(page.updated * 1000));
      lines.push(` ${date} [${title}]`);
    });
    lines.push("");
  });
  create_page(make_title(), lines);
};

function create_page(title, lines) {
  const body = encodeURIComponent(lines.join("\n"));
  window.open(`${project_root}/${title}?body=${body}`);
}

function pad(number) {
  if (number < 10) {
    return "0" + number;
  }
  return number;
}

function strftime(d) {
  return (
    d.getUTCFullYear() +
    "-" +
    pad(d.getUTCMonth() + 1) +
    "-" +
    pad(d.getUTCDate())
  );
}

const WAIT = { title: "Please wait...", image: null, onClick: () => null };
const onClick = () => {
  scrapbox.PageMenu(menu_title).addItem(WAIT);
  main();
  scrapbox.PageMenu(menu_title).removeAllItems();
};

scrapbox.PageMenu.addMenu({
  title: menu_title,
  image: "https://gyazo.com/11140c8b35b407c5d490a94ec6f2528f/raw",
  onClick,
});
```


old version
- 2018-05-25
    - [[ScrapboxSRS]]
    - [/customize/「過去のこの日」機能](https://scrapbox.io/customize/「過去のこの日」機能)

表記揺れ
- [[振り返り(Scrapbox)]]
