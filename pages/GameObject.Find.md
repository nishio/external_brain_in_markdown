
cs

```cs
GameObject.Find("Hand");
```

[Unity - Scripting API: GameObject.Find](https://docs.unity3d.com/ScriptReference/GameObject.Find.html)

[[マザーモノリス]]を名前で引っ張ってそこから子コンポーネントにアクセスしたりする
cs

```cs
var slides = GameObject.Find("t").GetComponent<MakeSlides>().slides;
```

