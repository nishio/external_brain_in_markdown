---
title: "Google Bertのtokenizerで濁音が取れる理由"
---

Google Bertのトークナイザにたとえば「モデル」という文字列を入れると濁音が取り除かれて「モテル」になってしまう。
これはアクセント記号を取り除くことを意図した下記の関数で、カテゴリ`Mn`(Mark, nonspacing)のものを全部捨てているが濁音記号などもこのジャンルに含まれるため。
python

```
  def _run_strip_accents(self, text):
    """Strips accents from a piece of text."""
    text = unicodedata.normalize("NFD", text)
    output = []
    for char in text:
      cat = unicodedata.category(char)
      if cat == "Mn":
        continue
      output.append(char)
    return "".join(output)
```


python

```
>>> chars = list(unicodedata.normalize("NFD", "モデル"))
>>> chars
['モ', 'テ', '゙', 'ル']
>>> [unicodedata.category(c) for c in chars]
>>> ['Lo', 'Lo', 'Mn', 'Lo']
```


