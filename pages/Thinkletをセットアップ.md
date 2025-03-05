---
title: "Thinkletをセットアップ"
---

from [[THINKLET]]
Thinkletをセットアップ

2024-12-13
[映像を撮ってみる | THINKLET App Developer](https://fairydevicesrd.github.io/thinklet.app.developer/docs/startGuide/useCamera)
:

```
 % scrcpy
scrcpy 3.0.2 <https://github.com/Genymobile/scrcpy>
* daemon not running; starting now at tcp:5037
* daemon started successfully
ERROR: Could not find any ADB device
ERROR: Server connection failed
```

電源入れ忘れ
:

```
% scrcpy
scrcpy 3.0.2 <https://github.com/Genymobile/scrcpy>
INFO: ADB device found:
INFO:     -->   (usb)  P16M116D5252823                 device  THINKLET_LC01
/opt/homebrew/Cellar/scrcpy/3.0.2/share/scrcpy/scrcpy-server: 1 file pushed, 0 skipped. 6.1 MB/s (90396 bytes in 0.014s)
[server] INFO: Device: [QUALCOMM] FD THINKLET LC01 (Android 8.1.0)
[server] WARN: Audio disabled: it is not supported before Android 11
INFO: Renderer: metal
WARN: Demuxer 'audio': stream explicitly disabled by the device
INFO: Texture: 1080x1920
2024-12-13 21:41:52.149 scrcpy[57506:30128462] +[IMKClient subclass]: chose IMKClient_Modern
2024-12-13 21:41:52.149 scrcpy[57506:30128462] +[IMKInputSession subclass]: chose IMKInputSession_Modern
```


- たまたま背景にチャットアプリが映り込んでしまった
    - まあ綺麗に読めるとはいえないものの、なんのプロジェクトでどんなチャンネルがあるかはわかる解像度だな


[録画アプリをつくってみる | THINKLET App Developer](https://fairydevicesrd.github.io/thinklet.app.developer/docs/startGuide/buildRecord)

[[Android Studio]]いれる
- [Android Studio とアプリツールのダウンロード - Android デベロッパー  |  Android Developers](https://developer.android.com/studio?gad_source=1&gclid=Cj0KCQiA0--6BhCBARIsADYqyL9cEDzcMG1XZUsilfZUySjdIpoL6qHqs7yxl-kde66B9Cs3_s0EjlwaAjGkEALw_wcB&gclsrc=aw.ds&hl=ja)

サンプルコード
[FairyDevicesRD/thinklet.app.developer](https://github.com/FairyDevicesRD/thinklet.app.developer/tree/main)

> Android Studioからデバッグ実行して、THINKLETにこのアプリをインストールします。
> ただし、初回デバッグ時は、Permissionを許可するような実装をしていませんので、何もできないアプリが起動するだけです。
build.gradleをデバッグ実行して何も起きないな？と思ったが、何もできないアプリが起動して終了したのか？
> 23:12:29: Executing...
> 23:12:30: Execution finished.

<img src='https://scrapbox.io/api/pages/nishio/o1 Pro/icon' alt='o1 Pro.icon' height="19.5"/>「build.gradleを実行する」だけでは、アプリはインストールされません。Android Studioの上部ツールバーなどから「Run」（または「Debug」）ボタンを押して、実際にアプリをビルドし、デバイス(THINKLET)へインストールしてください。
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>「Run」（または「Debug」）ボタン、グレーになってる
<img src='https://scrapbox.io/api/pages/nishio/o1 Pro/icon' alt='o1 Pro.icon' height="19.5"/>適切なRun Configurationがない
上部ツールバーから「Edit Configurations...」を選び、「app」モジュール用のRun Configurationがあるか確認。ない場合は新規作成する。
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
> 上部ツールバーから「Edit Configurations...」を選び、「app」モジュール用のRun Configurationがあるか確認。ない場合は新規作成する。
どうやるの？
<img src='https://scrapbox.io/api/pages/nishio/o1 Pro/icon' alt='o1 Pro.icon' height="19.5"/>
Android Studioのメニュー上部バーから「Run」→「Edit Configurations...」を開きます。
表示されたダイアログ左上の「＋（プラスボタン）」をクリックします。
一覧から「Android App」（もしくは「Android Application」）を選択します。
「Module」欄で自分のプロジェクトの「app」モジュールを選択します。
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
> 「Module」欄で自分のプロジェクトの「app」モジュールを選択します。
選べない
<img src='https://scrapbox.io/api/pages/nishio/o1 Pro/icon' alt='o1 Pro.icon' height="19.5"/>「app」モジュールが選べない原因は以下が考えられます。
プロジェクトのルートディレクトリでなく、個別ファイルやサブフォルダを開いている
クローンしたGitHubプロジェクト全体のルートディレクトリ（settings.gradleがあるディレクトリ）をAndroid Studioで「Open」してください。

できた！
![image](https://gyazo.com/a66536f17227cff98750a2900af35028/thumb/1000)
Android開発知ろうとなのでプロジェクトの開き方が間違ってたw

録画もできてた

[キーコンフィグを編集してみる | THINKLET App Developer](https://fairydevicesrd.github.io/thinklet.app.developer/docs/startGuide/buildKeyConfig)
`% adb shell am start -n com.example.fd.camera/com.example.fd.camera.MainActivity`
Starting: Intent { cmp=com.example.fd.camera/.MainActivity }

キーコンフィグもできた！
- これでPCがなくても録画開始できる

---
2025-03-05
[FairyDevicesRD/thinklet.app.lifelog: THINKLET ライフログアプリ](https://github.com/FairyDevicesRD/thinklet.app.lifelog)
