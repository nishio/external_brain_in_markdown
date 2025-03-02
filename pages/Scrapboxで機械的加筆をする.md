---
title: "Scrapboxで機械的加筆をする"
---

背景
- [/dominion](https://scrapbox.io/dominion)において、カードについて英語の文章を見て書くときも日本語の文章を見て書く時もある、どちらのリンクもつながって欲しい
- 手作業でいくつか作って見て「日本語のカード名称をタイトルに」「本文で英語名称のリンクを置く」という書き方に落ち着いた
- これを残りの数百枚に対してもやらなければ「日本語でも英語でもつながる」という便益を得られない
    - 手作業でやりたくないので機械的に生成する
- 機械生成したもので手で作ったものを上書きしたくない
    - 既にあるものに加筆すべきかしなくて良いかは確定していないので、とりあえず加筆する

実装
- まず現在のプロジェクトを更新日時つきでエクスポートする
- 英和一覧を見て
    - 既にページがあるなら加筆
    - ないなら古い日付で作成して加筆

python

```
import json
import from_enwiki
data = json.load(open('dominion.json'))

titles = [p["title"] for p in data["pages"]]
OLD = 946652400.0  # 2000-01-01
for line in open("jaen.txt"):
    ja, en = line.strip().split("\t")

    # generate contents
    lines = from_enwiki.parse(en)
    lines += ["", f"[ドミニオン Wiki https://wikiwiki.jp/dominiondeck/{ja}]"]

    if ja in titles:
        print("exists", ja, en)
        for page in data["pages"]:
            if page["title"] == ja:
                page["lines"] += lines

    else:
        page = dict(
            title=ja,
            lines=[ja] + lines,
            updated=OLD)
        data["pages"].append(page)

json.dump(data, open("dominion_new.json", "w"), indent=2)
```



