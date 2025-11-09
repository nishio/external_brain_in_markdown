---
title: "Azure Blob StorageにファイルがあるのにStorage Explorerで見えない"
---

[[Azure Blob Storage]]でバージョニングが無効なとき、[[Azure Storage Explorer]]で規定値の「アクティブなBLOB」ではファイルがないように見える
- Azure Storage Explorerでは表示フィルターを「すべてのBlobと現在のバージョンがないBlob」に設定すれば確認可能
- <img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>Blobは正常にHotティアのBlockBlobとして存在していますが、isCurrentVersionがNoneになっています。これが原因かもしれません。
- 一度表示するとアクティブなBLOBに選ばれるのか、その後は「アクティブなBLOB」でも表示されるようになった


Azure Blob Storage への接続と基本アップロードを検証するテストツールを追加 - by nishio
[https://github.com/digitaldemocracy2030/kouchou-ai/pull/711](https://github.com/digitaldemocracy2030/kouchou-ai/pull/711)
![image](https://gyazo.com/81698c6fdf2532005c5b1cd5d9ac2298/thumb/1000)

