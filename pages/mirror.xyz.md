---
title: "mirror.xyz"
---

[https://mirror.xyz](https://mirror.xyz)
<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>ウォレット接続でログインし、コンテンツは [[Arweave]] に恒久保存、メタデータは [[Ethereum]] 上に書き込む――という完全分散型アーキテクチャが売りです。

---
Metamaskを接続してみる
[[Polygon]]ネットワークでログインする感じかな
![image](https://gyazo.com/96fcb254a0d549db03c942491a89b77c/thumb/1000)
![image](https://gyazo.com/34669c5fa2fa319b74f7caf122288dd8/thumb/1000)
![image](https://gyazo.com/e2c7ae6de2702c61439105c192536341/thumb/1000)
[Protocol Rewards](https://support.mirror.xyz/hc/en-us/articles/21917161046804-Protocol-rewards)
- [https://chatgpt.com/s/t_688e0094bea481918fc388beb37b8e92](https://chatgpt.com/s/t_688e0094bea481918fc388beb37b8e92)

Entry published
- [https://mirror.xyz/0xd50c28f7Cda33859DFD34Bbab518cD50AcD5d610/eGyAROov06sZI2ZiqiHE-cOZZP9S7NTxeAfXNhChvZ0](https://mirror.xyz/0xd50c28f7Cda33859DFD34Bbab518cD50AcD5d610/eGyAROov06sZI2ZiqiHE-cOZZP9S7NTxeAfXNhChvZ0)

Profile page
- [https://mirror.xyz/0xd50c28f7Cda33859DFD34Bbab518cD50AcD5d610](https://mirror.xyz/0xd50c28f7Cda33859DFD34Bbab518cD50AcD5d610)

投稿するところで支払いが発生するかなと思ったがしなかった
コンテンツの保存費用はどこから出てくるのだろう？

<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>
まず結論 ―― Mirror で記事を投稿するときにガスやストレージ料を支払わなくて済んだのは、Mirror がバックエンドで Bundlr Network を通じて Arweave 代を「立て替え」ているから です。著者は無料で公開でき、後から NFT を収集する読者や Mirror のプラットフォーム手数料がネットワークに補填するかたちで恒久保存コストがまかなわれています。

1-1. 投稿自体は “ガスレス”
- Mirror は 2022 年に Writing NFT を導入し、「著者は無料で mint／公開できる」設計を採用しました。
- 公式ガイドでも「Writing NFT はデプロイ無料、必要なのは読者が収集するときのガスだけ」と明記されています。
- 実際の Arweave へのアップロードは [[Bundlr]] 経由で行われ、Optimism や Polygon など L2 上のメタトランザクションでガスを 0 に近づけています。

2. バックエンドで起きていること
- 2-1. [[Bundlr Network]]
    - Bundlr は Arweave の バンドル標準 [[ANS-104]] を使い、複数データをひとまとめにして Arweave L1 へ送るスケーリング層です。
    - ユーザーや dApp は ETH／MATIC／SOL など好きなトークンでストレージ料を前払い でき、Bundlr ノードが自動で AR に換えて支払います。
    - Mirror はこの Bundlr ウォレットに定期的に資金をチャージし、投稿時はその残高から数十〜数百 Wei 分を差し引くだけなのでユーザーには表示されません。
- 2-2. 1 記事あたりの実質コスト
    - Arweave ではテキスト 10 KB 程度なら 約 0.000002 AR（数十銭） で 200 年間保存が前払いできます。
    - これを Bundlr で一括処理するとさらに 1/100 ほどに圧縮できるため、Mirror が負担しても採算が合う水準です。


<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>[[Mint]]したりCollectしたりする人は何が嬉しいわけ？

<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>著者にとっては〈恒久保存＋収益化＋コミュニティ形成〉、コレクターにとっては〈所有権＋特典アクセス＋文化的／経済的リターン〉 が主な動機です。
[https://chatgpt.com/s/t_688e0afd14cc81919f67c68dbec39c1e](https://chatgpt.com/s/t_688e0afd14cc81919f67c68dbec39c1e)

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>著者は書いた時点で恒久保存されるの？それとも誰かが[[Lazy Mint]]してCollectした時点？

<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>Mirror で「公開 (Publish)」ボタンを押した瞬間、記事本文は Bundlr 経由で Arweave にアップロードされ、著者が 1 円も払わなくても即座に恒久保存されます。Writing NFT はその記事への所有証明トークンで、NFT のコントラクト自体は Lazy Mint 方式――最初の Collect ユーザが出たタイミングで初めてデプロイ & ミントされ、その人がガス代を負担します。したがって 保存は著者の公開時点、NFT 化は最初の Collect 時点 という二段構えです。
[https://chatgpt.com/s/t_688e1143ecfc8191b29f62372f0cc4e0](https://chatgpt.com/s/t_688e1143ecfc8191b29f62372f0cc4e0)

-----
著者側としてはあんまりデメリットはないな、
