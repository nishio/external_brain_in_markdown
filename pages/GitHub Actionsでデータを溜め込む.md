---
title: "GitHub Actionsでデータを溜め込む"
---

- 方法1: mainにcommitする
    - まず手軽
    - ソースコードのバージョン管理の間に大量のデータ更新コミットが突っ込まれるのでしばらく経ってから実装の続きをしようとなった時にコミットログを追いにくい
- 方法2: data branchを作ってcommitする
    - 一見良いように思うが、最新のコードで最新のデータに対して分析しようと思ってgit checkout dataしたらコードがdata branchを生やした時点まで巻き戻るのが罠
    - data ブランチを main の HEAD に rebase すればよい
        - git checkout data && git rebase main
        - しかしhistoryが変わるので git push -f することになる
        - 別の方法としては git merge main
    - [[OSS Weekly Reporter]]でこの構成をしたが安定するまでだいぶ苦労した
        - コードの修正がガンガン発生している間、最新のデータに対して最新の実装で何かしたい時にもれなく適切に上記の作業をしなければならない
        - data branchはGitHub Actionsが更新してくるので、うっかりpushし忘れたりした時にさらなるリカバリーが必要になる
- 方法3: date専用repositoryを作る([[data repo]])
    - これがいいんじゃないのかと2025-06-05現在思ってる
        - 疎結合にした方がいい
            - コードは公開しないけどデータはオープンとか、その逆とかもできる
    - 他のリポジトリにpushするためにはOrganizationの設定で許可した上で、その権限を持ってるPAT(Personal Access Token)を作る必要がある
        - GitHub Actions に自動付与される GITHUB_TOKEN は “workflow を含むリポジトリに限定” された権限しか持たない。
        - 組織設定 → Personal access tokens → Settings で「Allow access via personal access tokens」を有効化

- 方法x: releaseに置く
    - やったことあるけど複雑だよなという気がする
    - ファイルサイズの制約が緩いのがメリット

- 方法y: GistにUploadする
    - 大きくない「最新データ」をフロントエンドからfetchできるGET API的な形で配信したいときに使える

