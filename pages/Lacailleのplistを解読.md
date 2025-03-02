---
title: "Lacailleのplistを解読"
---

`$ plutil -p ~/Downloads/org.jpn.lacaille.Lacaille.plist`
:

```
{
  "bsemu" => 0
  "enabled" => 1
  "escemu" => 0
  "firstIgnoredSingleThumbL" => 1
  "layout" => [
    0 => {
      "ASCII - No shift" => <00ffff>
      "ASCII - With outer shift" => <3800ff>
      "No shift" => <20ffff>
      "With left shift" => <0d1fff>
      "With modifier key" => <00ffff>
      "With outer shift" => <3800ff>
      "With right shift" => <0920ff>
    }
...
```


[plistlib --- Mac OS X .plist ファイルの生成と解析 — Python 3.8.1 ドキュメント](https://docs.python.org/ja/3/library/plistlib.html)
:

```
{'NSStatusItem Preferred Position Item-0': 450.0,
 'layout': [{'With outer shift': b'8\x00\xff',
   'With right shift': b'\t \xff',
   'No shift': b' \xff\xff',
   'ASCII - With outer shift': b'8\x00\xff',
   'ASCII - No shift': b'\x00\xff\xff',
   'With left shift': b'\r\x1f\xff',
   'With modifier key': b'\x00\xff\xff'},
```


- [Lacaille/AppDelegate.m // loadPreferences](https://github.com/ikesato/Lacaille/blob/d5eaa843ee0ed9b6c81a9199439945bbeb971bf5/Lacaille/AppDelegate.m#L471)
    - [Lacaille/AppDelegate.m // convKeyData](https://github.com/ikesato/Lacaille/blob/d5eaa843ee0ed9b6c81a9199439945bbeb971bf5/Lacaille/AppDelegate.m#L604)
    - [keycode](https://github.com/ikesato/Lacaille/blob/d5eaa843ee0ed9b6c81a9199439945bbeb971bf5/Lacaille/AppDelegate.m#L525)

- [Lacaille/KeyTransformer.m // keyCodeToString](https://github.com/ikesato/Lacaille/blob/d5eaa843ee0ed9b6c81a9199439945bbeb971bf5/Lacaille/KeyTransformer.m#L71)
    - [keymap](https://github.com/ikesato/Lacaille/blob/d5eaa843ee0ed9b6c81a9199439945bbeb971bf5/Lacaille/KeyTransformer.m#L52)

c

```c
static NSString* keymap[0x80] = {
    @"a", @"s", @"d", @"f", @"h", @"g", @"z", @"x",
    @"c", @"v", @"[Section]", @"b", @"q", @"w", @"e", @"r",
    @"y", @"t", @"1", @"2", @"3", @"4", @"6", @"5",
    @"^"/* = */, @"9", @"7", @"-", @"8", @"0", @"["/* ] */, @"o",
    @"u", @"@"/* [ */, @"i", @"p", @"↩", @"l", @"j", @":"/* ' */,
    @"k", @";", @"]"/* \ */, @",", @"/", @"n", @"m", @".",
    @"⇥", @"␣", @"`", @"⌫", @"⌤"/* no def */, @"⎋", @"[R⌘]", @"⌘",
    @"⇧", @"⇪", @"⌥", @"⌃", @"[R⇧]", @"[R⌥]", @"[R⌃]", @"[fn]",
    @"[F17]", @"[K.]", @"<42>", @"[K*]", @"<44>", @"[K+]", @"<46>", @"⌧"/* Keypad */,
    @"[VolumeUp]", @"[VolumeDown]", @"[Mute]", @"[K/]", @"[K⌤]", @"<4d>", @"[K-]", @"[F18]",
    @"[F19]", @"[K=]", @"[K0]", @"[K1]", @"[K2]", @"[K3]", @"[K4]", @"[K5]",
    @"[K6]", @"[K7]", @"[F20]", @"[K8]", @"[K9]", @"¥", @"_", @"[K,]",
    @"[F5]", @"[F6]", @"[F7]", @"[F3]", @"[F8]", @"[F9]", @"[Eisu]", @"[F11]",
    @"[Kana]", @"[F13]", @"[F16]", @"[F14]", @"<6c>", @"[F10]", @"<6e>", @"[F12]",
    @"<70>", @"[F15]", @"[Help]", @"↖", @"⇞", @"⌦", @"[F4]", @"↘",
    @"[F2]", @"⇟", @"[F1]", @"←", @"→", @"↓", @"↑", @"<7f>",
};
```


- layout:0 = keycode:0 = keymap "a"
    - `"No shift" => <20ffff>`
        - 0x20 = 32 = keymap "u"
    - `"With right shift" => <0920ff>`: vu
    - `"With left shift" => <0d1fff>`: wo
- layout:48=@"¥"
- layout:49=@"_"
    - see [keycode](https://github.com/ikesato/Lacaille/blob/d5eaa843ee0ed9b6c81a9199439945bbeb971bf5/Lacaille/AppDelegate.m#L525)

フォーマットの解読はできたので[[keylayout]]から直接[[Lacaille]]のデータを吐くことができそう
