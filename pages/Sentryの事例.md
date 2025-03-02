---
title: "Sentryの事例"
---

Sentryを入れるとどんなことがわかるようになるかの事例

サーバでこんなエラーが6件くらい時間をおいて発生してる
![image](https://gyazo.com/bbb616fcd3c678da5ccd62282bf754a4/thumb/1000)

![image](https://gyazo.com/410a167470483ba6a31ff1341ca2a339/thumb/1000)
py

```
def initialize(mode, env):
    for x in plugins:
        if mode == x.MODE:
            env.log.append([0, x.START_QUESTION])
            env.state = x.START
            return
    else:
        raise ValueError(f"unknown mode {mode}")
```


あー、これはモードの指定をURLで受け取るようにしたせいで、URLの末尾にゴミがついてる時にエラーになるのだな

イコールではなくstartswithで判断するようにして、あとそれでも判断できなかったときには通常モードになるようにした
