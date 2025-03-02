---
title: "Lacailleでバックスペースをカウント"
---

バックスペースの回数を表示する改造が、多分ちゃんと動くようになった
上の文章を打ち込んだ後の表示がこれ
![image](https://gyazo.com/bd74ca145d3ffd15754d6104f4c39128/thumb/1000)
表示の更新は設定画面を開いたとき
アプリの再起動で数値のリセット
リセットボタンはつけてもいいかも

![image](https://gyazo.com/0c419ab35bc7bee38bd5edbaa3a22e98/thumb/1000)
修正多すぎ

リセットボタンをつけたので例文練習の間だけの計測結果を見れる
![image](https://gyazo.com/acd0f75cc65d1b7782977cc8350a8814/thumb/1000)
リリース [https://github.com/nishio/Lacaille/releases/tag/v2](https://github.com/nishio/Lacaille/releases/tag/v2)

-----memo

とりあえず[[Lacaille]]のソースに手を入れて、バックスペースの回数を積算してデバッグ出力するようにできたけど、どこに表示しようかな

objc

```
bool isCtrlH = (
    CGEventGetIntegerValueField(event, kCGKeyboardEventKeycode) == 4 &&
    CGEventGetFlags(event) == 0x40101);
bool isBackSpace = (
    CGEventGetIntegerValueField(event, kCGKeyboardEventKeycode) == 51 &&
    CGEventGetFlags(event) == 0x100);

if (type != kCGEventKeyDown && (isCtrlH || isBackSpace)){
    backSpaceCount++;
    debugOut(@"[BackSpace] %d\n", backSpaceCount);
}
```


---
objc

```
static CGEventRef keyUpDownEventCallback(CGEventTapProxy proxy, CGEventType type, CGEventRef event, void *refcon)
```


objc

```
    debugOut(@"[EV] Keycode=%d, Flags=<%llx>, Type=%d, gTargetPid=%d\n",
             (CGKeyCode)CGEventGetIntegerValueField(event, kCGKeyboardEventKeycode),	(CGEventFlags)CGEventGetFlags(event), type, gTargetPid);
```


ctrl H

```
[EV] Keycode=4, Flags=<40101>, Type=10, gTargetPid=9953
[RetP] Type=10 Keycode=4

[EV] Keycode=51, Flags=<100>, Type=10, gTargetPid=9953
[RetP] Type=10 Keycode=51
```

