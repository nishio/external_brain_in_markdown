
Unityの[[Input.mousePresent]]がOculus環境下では常にFalseかと思いきや、最初はFalseなのにトリガーを引いた後でTrueに変わるという現象が起きていた。PC環境かOculus環境かを切り分けるのにマウスの有無を使ってはいけない。

というわけでこんな感じになった:
cs

```cs
public static bool isOculus()
{
    return (
        OVRInput.GetActiveController() == OVRInput.Controller.RTrackedRemote ||
        OVRInput.GetActiveController() == OVRInput.Controller.LTrackedRemote);
}
```


