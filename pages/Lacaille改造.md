
自分用に色々試したいことがあるので[[Lacaille]]改造

- 本家 [https://lacaille.jpn.org/](https://lacaille.jpn.org/)
    - GPL
- ここからフォークした [https://github.com/ikesato/Lacaille](https://github.com/ikesato/Lacaille)
    - 2.2.2
- [[Lacailleでバックスペースをカウント]]: v1 v2
- 本家の2.3をマージした: v3

- [[丸括弧・波括弧をホームポジションで打ちたい]]
    - できた：[[英字モードでもシフト2種類使う]]

- [[Unicode記号を入力したい]]
    - [[改造LacailleのキーマップをJSONにした]]
    - [[🤔キー]]

---
objc

```
convTraditionalKeyData([(ViewDataModel *)obj getKeyData:0]), @"No shift",
convTraditionalKeyData([(ViewDataModel *)obj getKeyData:1]), @"With left shift",
convTraditionalKeyData([(ViewDataModel *)obj getKeyData:2]), @"With right shift",
convTraditionalKeyData([(ViewDataModel *)obj getKeyData:3]), @"With outer shift",
convTraditionalKeyData([(ViewDataModel *)obj getKeyData:4]), @"ASCII - No shift",
convTraditionalKeyData([(ViewDataModel *)obj getKeyData:5]), @"ASCII - With outer shift",
convTraditionalKeyData([(ViewDataModel *)obj getKeyData:6]), @"With modifier key",
```


objc

```
enum {
    KANA_NO_SHIFT,
    KANA_L_THUMB,
    KANA_R_THUMB,
    KANA_OUTER_SHIFT,
    ASCII_NO_SHIFT,
    ASCII_OUTER_SHIFT,
    WITH_MODIFIER,
    ASCII_L_THUMB,
    ASCII_R_THUMB
};
```


objc

```
static CGKeyCode viewTable[] = {
    6, 7, 8, 9, 11, 45, 46, 43, 47, 44, LAYOUT_KEY_COUNT - 1,   // 94
    0, 1, 2, 3, 5, 4, 38, 40, 37, 41, 39, 42,
    12, 13, 14, 15, 17, 16, 32, 34, 31, 35, 33, 30,
    18, 19, 20, 21, 23, 22, 26, 28, 25, 29, 27, 24, LAYOUT_KEY_COUNT - 2   // 93
};
```

これは文字キーを下段から書いたもの
94: kVK_JIS_Underscore
93: kVK_JIS_Yen: 0x5D
see [[kVK_JIS]]

objc

```
static inline void startTimer(NSTimeInterval negativeInterval) {
    [gLock lock];
    [gTimer invalidate];
    NSTimeInterval interval = prefTwait - negativeInterval;
    gTimer = [NSTimer scheduledTimerWithTimeInterval:(interval >= 0 ? interval : 0)
                                              target:self_
                                            selector:@selector(timerFired:)
                                            userInfo:(__bridge id)nil
                                             repeats:NO];
    [gLock unlock];
}

static inline void fireTimer() {
    [gTimer invalidate];
    [self_ timerFired:nil];
}
```


を
[[getKeyDataForOya]] Keycode=0, oya=1, ret=<0d1f>
[
[[getKeyDataForOya]] Keycode=93, oya=4, ret=<1e>
$
[[getKeyDataForOya]] Keycode=21, oya=5, ret=<3815ff>
[[{]]
[[getKeyDataForOya]] Keycode=93, oya=5, ret=<381eff>

a{{{{{{

asdfhgzx
objc

```
    // 同時判定時間を過ぎていたら親指キーを戻す
    if (!prefCshift && (gBuff == prefThumbL || gBuff == prefThumbR) &&
        [[NSDate date] timeIntervalSinceDate:gOyaKeyDownTimeStamp] > prefTwait) {
        unsigned char prevBuff = gBuff;
        CGEventFlags prevEventMasks = gEventMasks;
        switch(gBuff) {
            case kVK_Option: 
            case kVK_RightOption:
                  gEventMasks &= ~kCGEventFlagMaskAlternate;    break;
            case kVK_Command:
            case kVK_RightCommand:
                  gEventMasks &= ~kCGEventFlagMaskCommand;      break;
            case kVK_Shift: 
            case kVK_RightShift:        
            	gEventMasks &= ~kCGEventFlagMaskShift;        break;
            case kVK_CapsLock:
                gEventMasks &= ~kCGEventFlagMaskAlphaShift;   break;
            case kVK_Control:
            	gEventMasks &= ~kCGEventFlagMaskControl;      break;
        }
        startTimer(0);
        fireTimer();
        
        // 親指が修飾キーなら親指キーではなく修飾キーとしてもう一度押す
        if (prevEventMasks != gEventMasks) {
            myCGEventPostToPid(targetPid, CGEventCreateKeyboardEvent(source, prevBuff, YES));
            // yield しないと順序が逆になる
            [[NSRunLoop currentRunLoop] runUntilDate:[NSDate dateWithTimeIntervalSinceNow:0.05f]];
        }
    }

```


- [Auto Layout Guide: Working with Constraints in Interface Builder](https://developer.apple.com/library/archive/documentation/UserExperience/Conceptual/AutolayoutPG/WorkingwithConstraintsinInterfaceBuidler.html#//apple_ref/doc/uid/TP40010853-CH10-SW1)
