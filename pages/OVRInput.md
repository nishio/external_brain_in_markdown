---
title: "OVRInput"
---

[https://developer.oculus.com/documentation/unity/latest/concepts/unity-ovrinput/](https://developer.oculus.com/documentation/unity/latest/concepts/unity-ovrinput/)
> To use OVRInput, you must either:
- >  Include an instance of [[OVRManger]] anywhere in your scene; or
- >  Call OVRInput.Update() and OVRInput.FixedUpdate() once per frame at the beginning of any component’s Update and FixedUpdate methods, respectively.
しかしOVRManagerをSceneにドラッグドロップしようとしたらNGだった
これではないのか？？
![image](https://gyazo.com/9a5ce7224c7dcefda7043dccd79b5400/thumb/1000)

シーンではなく何らかのオブジェクト([[マザーモノリス]]とか)のコンポーネントとして追加するべきっぽい？
