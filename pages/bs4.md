---
title: "bs4"
---

[Beautiful Soup Documentation — Beautiful Soup 4.4.0 documentation](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)
python

```
data = open("quotes/1.html")
soup = bs4.BeautifulSoup(data, "lxml")

xs = soup("blockquote")
for x in xs:
    quote = x.text.strip()
    ref = x.nextSibling.nextSibling("a")[0]
    booktitle = ref.text.strip()
    s = ref.nextSibling
    page = re.search(r"(\d+)ページ", s).groups()[0]
    print(quote, booktitle, page)
```


