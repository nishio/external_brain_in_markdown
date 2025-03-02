---
title: "Pythonでローカル変数はグローバル変数より速い"
---

生Pythonでローカル変数のアクセスはグローバル変数へのアクセスより速い
- 競技プログラミングでPythonを使う人には有名な話だと思う
- 一つの変数に一千万回アクセスしてて、かつ数百msecの差で合否が分かれるような状況でのみ有用な話

python

```
def main():
  j = 0
  for i in range(10_000_000):
    j = i
  return j

print(main())
```

224msec
python

```
j = 0
for i in range(10_000_000):
  j = i
print(j)
```

573 ms
