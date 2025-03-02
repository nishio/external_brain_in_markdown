---
title: "GPUインスタンス"
---

ubuntuベースにした。

- tensorflow
    - [https://www.tensorflow.org/install/install_linux](https://www.tensorflow.org/install/install_linux)
    - `pip install --upgrade tensorflow-gpu` は `Could not find any downloads that satisfy the requirement tensorflow-gpu`
    - 説明の通りURL指定でインストールできた
    - 1.1.0

- scikit-learn
    - sudo pip install scikit-learn

- keras
    - sudo pip install keras


- スポットインスタンスが死んだときに途中結果が失われたりしないようにしたい
    - 同時に1インスタンスでしかマウントしないら
        - EBSマウントしとけばそれは消えない
    - 複数インスタンスでマウントしたいなら
        - EFS(ただし東京リージョンでは動かない)
        - 自分でNFSサーバを立てろ→VPCに入れば簡単
        - monit+rsync
        - 終了通知をウォッチする： [spot/termination-time](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-metadata.html)
        - [http://qiita.com/iogi/items/62f84e0ebfdc7afd9539](http://qiita.com/iogi/items/62f84e0ebfdc7afd9539)
        - [Dropbox](http://tm.root-n.com/server:dropbox:etc:dropbox_on_linux)
            - CLIでうまく入らない→諦めるか、X立ててVNC


[新機能 Amazon EC2のP2インスタンスが東京リージョンで使えるようになりました ｜ Developers.IO](http://dev.classmethod.jp/cloud/aws/ec2-p2-now-available-in-tokyo/)




EC2のGPUインスタンスにChainerを5行で入れて4行で動かす - 随所に主と作れば、立処皆真なり
[http://sla.hatenablog.com/entry/chainer_on_ec2](http://sla.hatenablog.com/entry/chainer_on_ec2)
AWSでサクッとChainerを使ってみる
[https://orientalrobotics.blogspot.jp/2015/07/awschainer.html](https://orientalrobotics.blogspot.jp/2015/07/awschainer.html)
Chainer on EC2スポットインスタンスの環境を、AWS Lambdaで用意する - Qiita
[http://qiita.com/pyr_revs/items/bf483b96cca6b01a9110](http://qiita.com/pyr_revs/items/bf483b96cca6b01a9110)
処理に時間がかかるスクリプトが終わった時にEC2インスタンスを止めるには - Masteries
[http://papix.hatenablog.com/entry/2016/06/02/131754](http://papix.hatenablog.com/entry/2016/06/02/131754)