---
title: "ScrapboxをOculus Goのブラウザで全画面表示"
---

![image](https://gyazo.com/cc5ddd452d0bb457c94b1a47a6e40111/thumb/1000)
[動画](https://www.facebook.com/nishiohirokazu/videos/10215545450485911/?notif_id=1528744657189025&notif_t=feedback_reaction_generic) [シェア先での議論](https://www.facebook.com/ohkubo.kohei/posts/10155752048016476) まとめ: [/nishio/大きい壁が欲しい](https://scrapbox.io/nishio/大きい壁が欲しい)

- [[Scrapbox]]をOculusのブラウザで[[全画面表示]]
- 全画面にしてもこの程度
    - 本当は[[球面180度]]ぐらいに配置したい
- Scrapbox自体にはプレゼンモードに遷移せずにフルスクリーンにする方法がないのでJSで全画面化する
    - [[webkitRequestFullscreen]] [https://developer.mozilla.org/en-US/docs/Web/API/Fullscreen_API](https://developer.mozilla.org/en-US/docs/Web/API/Fullscreen_API)
- なぜかタッチパッドでのスクロールが効かなくなる
script.js

```javascript
 var elm=document.createElement('span');
 elm.append("ZoomOut")
 elm.onclick = ()=>{
   		document.getElementsByClassName("page-list")[0].setAttribute('style', 'zoom: 0.5')
     	document.getElementsByTagName('body')[0].webkitRequestFullscreen()
 }
 document.getElementsByClassName("search-form")[0].parentElement.append(elm) 
```


続編 [[ScrapboxをWebVRで見る]]
