---
title: "LINKLETにライフログアプリを入れる"
---

![image](https://gyazo.com/6357de17b18027861f8c2373fdea8fbb/thumb/1000)サムネイル

from [[Thinkletをセットアップ]]
LINKLETにライフログアプリを入れる
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
- [[理解していない修正]]

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

2025-03-09
:

```
% adb shell ls /sdcard/DCIM/lifelog/19740105/
19740105_033437.gif
19740105_033437.raw
19740105_050124.raw
19740105_062813.raw
19740105_075501.raw
19740105_092149.raw
19740105_104838.raw
```

音声ファイルがたくさんあるな
`$ adb pull /sdcard/DCIM/lifelog/ ~/Downloads`
`$ ls -l ~/Downloads/lifelog/19740105`
:

```
total 10122120
-rw-r--r--  1 nishio  staff    11603521  3  9 23:52 19740105_033437.gif
-rw-r--r--  1 nishio  staff  1000000512  3  9 23:51 19740105_033437.raw
-rw-r--r--  1 nishio  staff  1000000512  3  9 23:53 19740105_050124.raw
-rw-r--r--  1 nishio  staff  1000000512  3  9 23:54 19740105_062813.raw
-rw-r--r--  1 nishio  staff  1000000512  3  9 23:52 19740105_075501.raw
-rw-r--r--  1 nishio  staff  1000000512  3  9 23:52 19740105_092149.raw
-rw-r--r--  1 nishio  staff   130837248  3  9 23:53 19740105_104838.raw
```

なるほど音声ファイルは1GBで分割か
rawファイルは[[Audacity]]でインポートするか、ffmpegで変換することができる
Audacityで観察してみよう
![image](https://gyazo.com/0030b9dad8b2ead55b9b0c8743237664/thumb/1000)

![image](https://gyazo.com/bfc03d2ee156b77269b098a1ade20ab6/thumb/1000)
1GBで1時間半
MP3にすると120MB
[[NotebookLM]]に投げる
- ごく一部
    - ![image](https://gyazo.com/7afc773fe6d2de8af3911e2f920ab06e/thumb/1000)
    - "野田クリスタル", "プルラリティ"などの言葉の文字起こしには困難があるが「そうそう、そういう話したよね！」という感じで、こういう会で一気にたくさん話しすぎて記憶が溢れてしまうことがよくあるので、どんなことを話したか振り返れることの価値は高そう
    - 興味深い話だけ掘り下げて解説させることができるはず

2025-03-10
![image](https://gyazo.com/5c1db5e609309c0028fcfe7d571658c4/thumb/1000)
- 今度やる時に考える

bash

```
for f in ~/Downloads/lifelog/19740105/*.raw; do
  ffmpeg -f s16le -ar 48000 -ac 2 -i "$f" "${f%.raw}.wav"
done
```


[https://app.devin.ai/sessions/02e8ade3a448425b9c6c178e0db0e236](https://app.devin.ai/sessions/02e8ade3a448425b9c6c178e0db0e236)

2025-03-15
> [nishio](https://x.com/nishio/status/1900559337145213210) あんまりいい写真がないけど先日の未踏会議未踏ナイトではFairyDevices社さんから貸与いただいてる首かけAndroidデバイスのLINKLETをつけて活動していました。7時間半つけっぱなしにしてたけど問題なく稼働して音声と画像が撮れていました #未踏会議
>  ![image](https://pbs.twimg.com/media/GmAkIijbsAAjhKz?format=png&name=small#.png)

> [nishio](https://x.com/nishio/status/1900559891317903762) 講演してる側の視点
>  ![image](https://pbs.twimg.com/media/GmAlIeLawAA_R46?format=png&name=medium#.png)

> [nishio](https://x.com/nishio/status/1900560416574672982) 懇親会
>  @ukkaripon
>  @teramotodaiki
>  ![image](https://pbs.twimg.com/media/GmAlkf6aoAAK__o?format=png&name=medium#.png)

> [nishio](https://x.com/nishio/status/1900562039598456988) 懇親会じゃなくて二次会だった。懇親会でも色々な人が映ってて「そうそう、なになにさんと話したんだった」ってなってよかった。そして単なるライフログカメラと違ってマイクが5~6個も乗ってるので後から処理すれば自分と相手の声を分離できそうなのが良い。

