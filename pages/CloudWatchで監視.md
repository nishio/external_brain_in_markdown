---
title: "CloudWatchで監視"
---

from [[2024年夏Polis祭り]]
CloudWatchで監視

1:
ビルド待ちの間に監視について聞く
<img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>EC2で動かしているサーバの負荷を手軽に監視する手段について、具体的にいくつかの方法を挙げます。
- Amazon CloudWatch:
    - 設定: AWSマネジメントコンソールからCloudWatchダッシュボードにアクセスし、監視したいメトリクスを選択。
    - 機能: CPU使用率、ディスクI/O、ネットワークトラフィック、メモリ使用率（カスタムメトリクスとして設定可能）などをリアルタイムで監視。
    - アラート: 特定の閾値を超えた場合に通知を受け取るよう設定可能。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>Amazon CloudWatchコンソール初見、何をしたらいいか

ChatGPT
Amazon CloudWatchコンソールを初めて使う場合、以下のステップで設定を進めると良いでしょう。

1. CloudWatchコンソールにアクセス
AWSマネジメントコンソールにログインします。
サービス一覧から「CloudWatch」を選択します。
2. メトリクスの確認
左側のナビゲーションペインで「メトリクス」をクリックします。
「すべてのメトリクス」タブを選択し、表示されるリソース一覧から監視したいEC2インスタンスのメトリクスを選択します。
一般的なメトリクスにはCPU使用率（CPUUtilization）、ディスク読み書き（DiskReadOps, DiskWriteOps）、ネットワークトラフィック（NetworkIn, NetworkOut）などがあります。
3. ダッシュボードの作成
左側のナビゲーションペインで「ダッシュボード」をクリックし、「ダッシュボードの作成」を選択します。
ダッシュボードに名前を付け、「追加」をクリックしてウィジェットを追加します。
「ラインチャート」や「数値」などのウィジェットを選択し、監視したいメトリクスを追加します。
4. アラームの設定
左側のナビゲーションペインで「アラーム」をクリックし、「アラームの作成」を選択します。
「メトリクス」から監視したいメトリクスを選択し、条件（閾値）を設定します。
例：CPU使用率が80％を超えた場合にアラームをトリガーする。
通知先（SNSトピック）を設定して、アラームがトリガーされた際にメールやSMSで通知を受け取るようにします。
5. CloudWatch Agentのインストール（オプション）
メモリ使用率など、デフォルトでは取得できないメトリクスを監視するためにCloudWatch Agentをインストールします。
EC2インスタンスにSSHでログインし、以下のコマンドを実行してCloudWatch Agentをインストールします。
bash
コードをコピーする
sudo yum install amazon-cloudwatch-agent
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-config-wizard
ウィザードに従って設定ファイルを作成し、CloudWatch Agentを起動します。
bash
コードをコピーする
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a fetch-config -m ec2 -c file:/path/to/your/config.json -s
これらの手順を踏むことで、Amazon CloudWatchコンソールを使ってEC2インスタンスのパフォーマンスを監視する設定ができます。


ふむふむ
![image](https://gyazo.com/a66d0511dc03fa9b6ee8e5b1d0577584/thumb/1000)

なるほど
![image](https://gyazo.com/1557f93bca949479e4a245b21371bc6d/thumb/1000)


from [[2024年夏Polis祭り]]
[[CloudWatchで監視]]
2:
ClaudWatch

:

```
Current config as follows:
{
        "agent": {
                "metrics_collection_interval": 60,
                "run_as_user": "cwagent"
        },
        "metrics": {
                "metrics_collected": {
                        "disk": {
                                "measurement": [
                                        "used_percent"
                                ],
                                "metrics_collection_interval": 60,
                                "resources": [
                                        "*"
                                ]
                        },
                        "mem": {
                                "measurement": [
                                        "mem_used_percent"
                                ],
                                "metrics_collection_interval": 60
                        }
                }
        }
}
```


:

```
$ sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -m ec2 -a status
{
  "status": "stopped",
  "starttime": "",
  "configstatus": "configured",
  "version": "1.300041.0b681"
}
```

あってるのかよくわからない
- ![image](https://gyazo.com/9b7b91a21e6c4bf8d31e504fc374c779/thumb/1000)
    - 0すらこなくなってるじゃん！

