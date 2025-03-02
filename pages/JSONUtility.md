---
title: "JSONUtility"
---

ToJsonにVector3のArrayを渡しても`{}`になる
> passing an array to this method will not produce a JSON array containing each element
[https://docs.unity3d.com/ScriptReference/JsonUtility.ToJson.html](https://docs.unity3d.com/ScriptReference/JsonUtility.ToJson.html)

直接Arrayを[[シリアライズ]]することはできないが、Arrayをフィールドに持つクラスのインスタンスはシリアライズできる

それをJsonUtil.FromJson<Foo>しようとするとコンパイルエラー。あらかじめ作っておいたFooのインスタンスfooに対してJsonUtil.FromJsonOverwrite(json, foo)なら成功する。

シリアライズ時にプロパティのGetterが呼ばれないっぽい罠
- 明示的に呼ぶ

[[Unity]]
