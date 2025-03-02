
素朴に実装すると$O(N^2\log N)$の[[接尾辞配列]]を$O(N)$で作る方法

- 接尾辞配列とは
python

```
data = "abracadabra$"

buf = []
for i in range(len(data)):
    buf.append((data[i:], i))

buf.sort()

for x in buf:
    print(x)
```

- 接尾辞配列ができると特定のキーワードの出現場所を二分探索で効率よく発見できる
- 先頭文字に対するバケットソートを使う

難しい

噛み砕いた解説
[http://shogo82148.github.io/homepage/memo/algorithm/suffix-array/](http://shogo82148.github.io/homepage/memo/algorithm/suffix-array/)

わかりやすい？解説
[https://mametter.hatenablog.com/entry/20180130/p1](https://mametter.hatenablog.com/entry/20180130/p1)
