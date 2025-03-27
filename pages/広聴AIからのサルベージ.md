---
title: "広聴AIからのサルベージ"
---

2025-03-27
Azure環境の広聴AIに大きなデータを入れたらしばらく実行された後でエラーになってしまった
どういう原因で失敗したのかを調べるためにAzure Container Appの中の中間データを取り出したい
![image](https://gyazo.com/7f58f3e0d85f1b677e529026b56f4eb8/thumb/1000)

注:
- [成功したレポートのデータを取り出すスクリプト](https://github.com/digitaldemocracy2030/kouchou-ai/blob/main/scripts/fetch_reports.py)は3/25に作ってある
- 今回は中間データを取り出したいという話で、これは大部分の人には必要ない作業
- o3は「<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>Azureの環境なら、Blob Storageへのアップロードが唯一現実的です」とかいってくる面倒なシチュエーションを無理やりハックするメモです
- これをやっている間、管理画面や結果表示画面はもちろんみんな動かなくなる
- 普通の24時間運用するWebサービスの運用としてはあり得ないことをするのだけど、今回は顧客向けに24時間提供している状況ではないのでやってる

## コンテナにbashで入る
:

```
az containerapp exec \
  --name <コンテナアプリ名> \
  --resource-group <リソースグループ名> \
  --container <コンテナ名> \
  --command "/bin/bash"
```



## zipしてport=8001でserveする
`$ apt update`
`$ apt install zip`
`$ cd broadlistening/pipeline`
`$ zip -r outputs.zip outputs`
`$ python -mhttp.server 8001`


## apiサーバのイングレスの設定を一時的に変える
APIサーバは普通にHTTPSでアクセスすると`{"status":"ok"}`と返してくる
これはAzureがリクエストを8000番で動いているHTTPサーバに転送している
この設定を一時的に8001番に変える

![image](https://gyazo.com/44c170eaf8c7121a86c335f0c8e5708a/thumb/1000)![image](https://gyazo.com/fb6776b7b932f9b01ef6737d327decf8/thumb/1000)

これでAPIサーバにアクセスした時に先ほど作ったresults.zipが見えて、ダウンロードできるようになる。
![image](https://gyazo.com/0b3066753a9f09a68b6acddbaef31a5e/thumb/1000)

ダウンロードし終わったら忘れずに元に戻しておく

## 余談: 結果を見てみる
![image](https://gyazo.com/4b04de66ecbc24d92239439361f8420c/thumb/1000)![image](https://gyazo.com/14a017fe6449b073fd8a33ac264f0f53/thumb/1000)
通常の成功したレポートは左のようになるが、今回のは右
args.csvにextractionの結果の25000~件5.2MBのデータが出力されている
nasukaさんの推測ではOut of Memoryじゃないかということだったが、多分そうなのだろうという感じ

embeddingでtext-embedding-3-smallを使ってて、1件あたり1536次元のfloat32になる。
それをPythonの`list[float]`で扱ってる
Pythonのfloatは倍精度float64で8バイトなので合計 = 1536 × 8 = 12,288バイト（約12KB）
25000件ならざっくり300MB
メモリ1GBのコンテナだとアプリケーションが使える余裕がそんなにはないってことなんだろうな
2GBなら余裕なはず