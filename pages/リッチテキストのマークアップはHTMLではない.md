---
title: "リッチテキストのマークアップはHTMLではない"
---

![image](https://gyazo.com/8cb4cf8daed4aab2f7dfaf41affa1411/thumb/1000)
タグの見かけが一見HTMLっぽいのでHTMLだと早合点してしまったが、そうではない。
誤:

```
<font size="28">02</font>
```

正:

```
<size="28">02</size>
```

![image](https://gyazo.com/7412fb08ff62869e2c393507c1f035a6/thumb/1000)
see [リッチテキスト - Unity マニュアル](https://docs.unity3d.com/jp/current/Manual/StyledText.html)

[[リッチテキスト]]の[[マークアップ]]
[[Text]]
