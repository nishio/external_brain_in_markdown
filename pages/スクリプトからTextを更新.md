
![image](https://gyazo.com/ecfc18d06bb92fd64db60ba69102ee49/thumb/1000)

cs

```cs
GameObject.Find("FooText").GetComponent<Text>().text = x.ToString();
```

テキスト自体に一意な名前"FooText"を振ってある場合。

Findで[[GameObject]]を取った後Textにキャストしようとしたがそれは勘違いで、そのGameObjectにComponentとしてTextが入っているので、それを[[GetComponent]]すればよい。

テキストを持っている親オブジェクトに名前がある場合
cs

```cs
GameObject.Find("Foo").GetComponentInChildren<Text>().text = x.ToString();
```


- スクリプトから[[Text]]を更新
- [[デバッグ]]
