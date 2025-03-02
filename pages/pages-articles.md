
[[Wikipedia]] dump pages-articles

python

```
def getPages():
    inPage = False
    ret = []
    for line in open(filename):
        if line.strip() == "<page>":
            ret.append(line)
            inPage = True
        elif line.strip() == "</page>":
            ret.append(line)
            yield ret
            ret = []
            inPage = False
        if inPage:
            ret.append(line)
```


