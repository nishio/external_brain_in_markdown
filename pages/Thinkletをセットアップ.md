---
title: "Thinkletをセットアップ"
---

![image](https://gyazo.com/6357de17b18027861f8c2373fdea8fbb/thumb/1000) サムネイル用

from [[THINKLET]]
Thinkletをセットアップ
[[LINKLET]]

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
Android開発素人なのでプロジェクトの開き方が間違ってたw

録画もできてた

[キーコンフィグを編集してみる | THINKLET App Developer](https://fairydevicesrd.github.io/thinklet.app.developer/docs/startGuide/buildKeyConfig)
`% adb shell am start -n com.example.fd.camera/com.example.fd.camera.MainActivity`
Starting: Intent { cmp=com.example.fd.camera/.MainActivity }

キーコンフィグもできた！
- これでPCがなくても録画開始できる

---
2025-03-05
[FairyDevicesRD/thinklet.app.lifelog: THINKLET ライフログアプリ](https://github.com/FairyDevicesRD/thinklet.app.lifelog)

![image](https://gyazo.com/d5ef7d577255907bce3ff715364a13e9/thumb/1000)
一旦スルー

> Could not GET '[https://maven.pkg.github.com/FairyDevicesRD/thinklet.app.sdk/ai/fd/thinklet/sdk-audio/0.1.6/sdk-audio-0.1.6.pom'.](https://maven.pkg.github.com/FairyDevicesRD/thinklet.app.sdk/ai/fd/thinklet/sdk-audio/0.1.6/sdk-audio-0.1.6.pom'.) Received status code 401 from server: Unauthorized
<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>
このエラーは、GitHub Packagesからライブラリを取得する際の認証情報が不足しているために発生しています。以下の手順で対処してください。
GitHub Personal Access Tokenの作成
- GitHubの「Settings」→「Developer settings」→「Personal access tokens」で新規トークンを作成します。
- 作成時に必ず「read:packages」権限を付与してください。
local.propertiesに認証情報を追加 ...

READMEに書いてあったやつだな

![image](https://gyazo.com/2bc6018940666acaa8c1c3ff63b381f9/thumb/1000)
<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>
> 対応デバイス上でテストを行ってください。
> adb devices コマンドで認識されているか確認します。

`% adb devices`
List of devices attached
emulator-5554	device

あー接続して赤ランプになってるだけでは起動してないか、そうか
起動して水色→緑になった

`% adb devices`
List of devices attached
P16M116D5252823	device
emulator-5554	device

OK

---
:

```
2025-03-07 13:58:51: Launching app on 'QUALCOMM THINKLET LC01'.
Starting: Intent { act=android.intent.action.MAIN cat=[android.intent.category.LAUNCHER] cmp=ai.fd.thinklet.app.lifelog/.MainActivity }

Open logcat panel for QUALCOMM THINKLET LC01 (P16M116D5252823)
Connected to process 3550 on device 'qualcomm-thinklet_lc01-P16M116D5252823'.
```


できた

![image](https://gyazo.com/12f76352976fb62153a2d6d22e321f64/thumb/1000)

懇親会での会話を拾うなら[[ビームフォーミング]]しない方がいいという話
- [FairyDevicesRD/thinklet.app.sdk: SDK for THINKLET application](https://github.com/FairyDevicesRD/thinklet.app.sdk?tab=readme-ov-file#%E8%A9%A6%E9%A8%93%E7%9A%84%E6%A9%9F%E8%83%BD-%E9%9F%B3%E5%A3%B0%E5%87%A6%E7%90%86)
- [disable_beamforming.patch](https://gist.github.com/nishio/1295526320d27da8c6aea80d75525f97)


全然何も保存されてなかった、パーミッションの設定が必要ね
![image](https://gyazo.com/81f992c6b46314ca99c2a3223e98aa3c/thumb/1000)![image](https://gyazo.com/10bd32578804bd182d77e1f90d8bcaef/thumb/1000)

`$ adb shell am start -n ai.fd.thinklet.app.lifelog/.MainActivity --ez enabledMic true`
`$ adb shell ls /sdcard/DCIM/lifelog/19740103/              `
19740103_045124.raw
19740103_045125.gif

<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>
転送方法として、主に以下の2通りがあります。
- adb コマンドを使う方法
    - ターミナルで以下のコマンドを実行すると、指定ディレクトリに保存されたファイルがPCにコピーされます。
    - `$ adb pull /sdcard/DCIM/lifelog/ [転送先のPC上のディレクトリパス]`

- MTPモードを使う方法
    - デバイスをUSB接続し、通知領域から「ファイル転送（MTP）」モードに切り替えます。
    - PCのエクスプローラー（Windowsの場合）やFinder（Macの場合）でデバイスの内部ストレージにアクセスし、DCIM/lifelog/ フォルダ内のファイルをコピーします。

:

```
% adb shell ls /sdcard/DCIM/lifelog/19740103/              
19740103_045124.raw
19740103_045125.gif
% adb pull /sdcard/DCIM/lifelog/ ~/Downloads 
/sdcard/DCIM/lifelog/: 2 files pulled, 0 skipped. 27.3 MB/s (78614272 bytes in 2.748s)
```


`$ ffmpeg -f s16le -ar 48000 -ac 2 -i ~/Downloads/lifelog/19740103/19740103_045124.raw output.wav `

実際につけて歩いて喋ってを試してみないとだな

2025-03-08
- [[LINKLET]]のテスト運用
    - マフラーしたらダメかなと思ったが意外と問題ない
    - ![image](https://gyazo.com/6357de17b18027861f8c2373fdea8fbb/thumb/1000)

:

```
% adb shell ls /sdcard/DCIM/lifelog/19740104
19740104_005846.raw
% adb shell ls /sdcard/DCIM/lifelog/19740103
19740103_045124.raw
19740103_045125.gif
19740103_233158.raw
19740103_233159.gif
```


ふむ？これは内部的に日付が変わったのか？
`% adb pull /sdcard/DCIM/lifelog/ ~/Downloads`
19枚くらいの画像が撮れていた
5分に1回くらいかな？

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>写真は何分に一回撮られてるかな？調べて
<img src='https://scrapbox.io/api/pages/nishio/Roo/icon' alt='Roo.icon' height="19.5"/>調査結果をまとめると：
1. デフォルト設定：300秒（5分）に1回
    - LifeLogArgs.ktの21行目で定義されています
    - `intervalSeconds = max(bundle?.get("intervalSeconds")?.toString()?.toIntOrNull() ?: 300, 10)`
2. 最小間隔：10秒
    - 同じくLifeLogArgs.ktの21行目で、最小値として10秒が設定されています
3. 設定ファイルによる設定：
    - `keyConfigs/2592_1944_withMic.json`：120秒（2分）に1回
    - `keyConfigs/1440_1080.json`：30秒に1回

実際にどの設定が使用されているかは、アプリの起動方法によって異なります。アプリが設定ファイルを使用して起動されている場合は、その設定ファイルの間隔が適用されます。設定なしで起動されている場合は、デフォルトの300秒（5分）が適用されます。

---

音声の具合に関しては明日撮ってみないとだな〜

