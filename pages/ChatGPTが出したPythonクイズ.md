---
title: "ChatGPTが出したPythonクイズ"
---

> [@tokoroten](https://twitter.com/tokoroten/status/1691819049770955219?s=20): ううう・・・デコレータ使ったことない・・・
> ![image](https://gyazo.com/ade54a80490ce69a33145d8522f54faf/thumb/1000)

なかなかいい問題だねw

python

```
# fill here
func()
func()
func()
```

output

```
func called
1 times called
func called
2 times called
func called
3 times called
```


解答

python

```
def deco(func):
    count = 0

    def wrapper():
        nonlocal count
        func()
        count += 1
        print(count, "times called")

    return wrapper


@deco
def func():
    print("func called")


func()
func()
func()
```



