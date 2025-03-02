
2022-01-20
- いきさつ: [[ScrapboxAutoTrans開発日記2022-01-20]]
- [/intellitech-en](https://scrapbox.io/intellitech-en)をこのプロジェクトにマージする
- ![image](https://gyazo.com/b07e82d4ba1e17841a60b1cd53a670c6/thumb/1000)
- ![image](https://gyazo.com/92f28c5bf9c53d50ef15ad9d5c6575bc/thumb/1000)
    - 意外なものが衝突するな…
    - とりあえずインポートしてからどうするか考えるために日本語の方のタイトルを変更しておくか
    - prefix: `(衝突)`

add_icon_on_all_pages.py

```
import json
IN_FILE = "intellitech-en.json"
OUT_FILE = "intellitech-en-out.json"
ICON = "[en.icon]"
data = json.load(open(IN_FILE))
for p in data["pages"]:
    p["lines"].append({"text": ICON})

json.dump(data, open(OUT_FILE, "w"))
```


できた

衝突ページの解決
- 大体のページは英語版が主
- George Edward Pelham Boxだけどうするか迷った
    - 日本語のページにもリンクがある
    - 両方残すことにした


[[pIntEn]]
