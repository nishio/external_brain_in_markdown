
メモ

js

```javascript
Array.from(document.querySelectorAll(".o-textNote__link")).map(x=>x.href).join(" ")
```


`wget -i`はつかえない

requestsでならできる
python

```
def crawl():
    urls = open("urls.txt").read().strip("'").split()
    for url in urls:
        print(url)
        fn = url.replace(PREFIX, "")
        r = requests.get(url)
        print(r)
        open(f"data/{fn}.html", "w").write(r.text)
```


figureによる他のページの埋め込み、iframeなのでめんどくさい
- URLの識別子部分を使って2-hopsで繋がればそれでいいか
