---
title: "Raspberry Pi"
---

- 普段の接続
    - 6,8,10でシリアルコンソール接続
    - 1,3,5,9でI2C
![image](https://gyazo.com/c126d73bb528a4fd5cde51f3b5849401/thumb/1000)

2018-09-09 old title [[ラズパイ]]
[[Builderscon 2018]]
- [https://speakerdeck.com/kazuph/builderscon-tokyo-2018-day1-chan-ye-degatili-yong-sareruraspberry-pifalsehua](https://speakerdeck.com/kazuph/builderscon-tokyo-2018-day1-chan-ye-degatili-yong-sareruraspberry-pifalsehua)
- 組み込みでもCI
    - リポジトリにpushするとJenkinsがバイナリ作る
    - 設置済みデバイスのマイコンにラズパイ直結(JTAG)
    - ラズパイがマイコンに書き込む
        - ラズパイでJenkinsスレーブが動く
        - J-LinkのARMバイナリがある
        - J-LinkがARM用バイナリを出しているのでRasPiからマイコン書き込みができる
- ラズパイがログを収集してネットに投げる

- ホビー目的ではWifiに繋がるESP系が人気だが、電気を食う。
    - nRF52っていうBLEマイコンが良い
- サーボやセンサーに関してはArduinoが得意
- シリアルの上にJSONを流す
    - Arduinoライブラリがある

