
日本語版エンジニアの知的生産術のScrapbox化したプロジェクトの全ページに「翻訳まだ」タグをつけて英訳用プロジェクトを作りたかったので書いた。簡単すぎてツールとして公開するほどのことではないのでここに貼っておく。

python

```
import json
data = json.load(open("/Users/nishio/Downloads/test-scrapbook-20181215.json"))
for page in data["pages"]:
    page["lines"].extend(["", "[翻訳まだ]"])

json.dump(data, open("out.json", "w"))
```

