---
title: "mimi"
---

Fairy Devicesの提供する音声認識関連のサービス
無料のお試し:
- > 読み込めるファイル形式はrawファイルです。サンプリングレート16kHz、量子化ビット16bit、PCM、モノラル（1ch）。容量は5MBまでです。
- [https://console.mimi.fd.ai/console/v1/speechrecognition](https://console.mimi.fd.ai/console/v1/speechrecognition)

- 16kHzで16bit(2byte)なので1秒あたり32,000B、150秒で4,800,000B
    - `$ sox in.mp3 -c 1 -r 16000 out.raw trim 0 150`
        - [[SoX]]
