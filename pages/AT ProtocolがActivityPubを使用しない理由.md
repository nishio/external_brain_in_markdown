---
title: "AT ProtocolがActivityPubを使用しない理由"
---

2023-07-29
- なんでだろ？と思ってGPT4に聞いてみたら、解答になるほどと思ったのでメモしておく

<img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>[[AT Protocol]]が[[ActivityPub]]を使用しない理由はいくつかあります：
- 設計哲学：
    - ActivityPubは、分散サーバーネットワーク上でコンテンツを作成、更新、削除するためのプロトコルです。主にサーバー間の相互作用を処理しますが、ユーザーやアプリケーションがデータをどのように管理し、このネットワークとどのように相互作用すべきかについては扱っていません。
    - 一方、ATプロトコルの設計は、より細かい[[データ所有権]]と取り扱い、連携、相互運用に関する制御を含み、ユーザーの制御とプライバシーに重点を置いています。

- 異なるデータモデル：ATプロトコルとActivityPubは、異なるデータモデルを使用しています。
    - ATプロトコルは、データが署名付きのデータリポジトリに保管され、さまざまなサーバー間で同期できるモデルを使用しています。また、Lexiconと呼ばれるスキーマネットワークを提供して、異なるサーバー間でデータを統一します。
        - 確かに。スキーマが固定されてると発展性がないね<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
            - [[AT ProtocolのLexicon]]を詳しく調べてみる必要がありそうだ
    - 一方、ActivityPubは、データがサーバー間で配布されるインボックス/アウトボックスモデルを使用し、グローバルスキーマを提供していません。

- 連携の違い：
    - ActivityPubは、サーバーがピアとして相互作用し、ActivityPubプロトコルを使用して通信する単一の連携モデルを持っています。
    - 一方、ATプロトコルは、ユーザーデータとイベントをそれぞれ処理するための個人データサーバー（PDS）とビッググラフサービス（BGS）を使用するより複雑な連携モデルを使用しています。
    - この区別は、スケールとユーザーの選択を実現することを目指しています。

- アカウントの移植性：ATプロトコルはアカウントの移植性を重視しており、DIDと署名付きデータリポジトリのシステムを使用して、ユーザーがサーバーの介入なしにデータを新しい個人データサーバーに移行できるようにしています。これはActivityPubの組み込み機能ではありません。
    - DIDとは[[分散型ID]]のこと<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>

- アルゴリズムの選択：ATプロトコルは、ユーザーがコンテンツの発見と検索のためのアルゴリズムを自由に選択できるように設計されています。これはActivityPubが提供する機能ではありません。

全体的に言えば、ATプロトコルがActivityPubを使用していないわけではなく、ATプロトコルは異なる目標と哲学をもとに設計されたため、プロトコルのアーキテクチャが異なっています。ActivityPubは特定の種類の分散アプリケーションにとって素晴らしいツールですが、ATプロトコルの設計者たちは明らかに彼らが達成したいと考えていたビジョンが異なっていたようです。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>Why AT Protocol doesn't use ActivityPub?
<img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>
The Authenticated Transfer Protocol (AT Protocol) does not use ActivityPub for a few reasons:

Design Philosophy: ActivityPub operates on a fundamentally different philosophy than the AT Protocol. ActivityPub is a protocol for creating, updating and deleting content on a distributed server-to-server network. It mainly handles the server to server interactions, but does not deal with how users and applications manage their data or how they should interact with this network. On the other hand, AT Protocol's design involves more granular control over data ownership and handling, federation, and interoperation with a larger focus on user control and privacy.

Different data model: AT Protocol and ActivityPub use different data models. AT Protocol uses a model where data is kept in signed data repositories that can be synced across different servers and provides a schema network called Lexicon to unify data across different servers. On the other hand, ActivityPub uses a model where data is distributed across servers using an inbox/outbox model and does not provide a global schema.

Different approaches to federation: ActivityPub has a single federation model where servers are peers and communicate using the ActivityPub protocol. AT Protocol uses a more complex federation model with Personal Data Servers (PDS) and Big Graph Services (BGS) to handle user data and events respectively. This distinction is meant to achieve scale and user choice.

Account portability: AT Protocol emphasizes account portability, allowing users to migrate their data to a new Personal Data Server without the server's involvement, using a system of DIDs and signed data repositories. This isn't a built-in feature of ActivityPub.

Algorithmic choice: AT Protocol is designed to allow users to choose their own algorithms for content discovery and search, which is not a feature provided by ActivityPub.

Overall, it's not so much that AT Protocol doesn't use ActivityPub; rather, AT Protocol was designed with different goals and philosophies in mind, leading to a different protocol architecture. ActivityPub is a wonderful tool for certain kinds of decentralized applications, but the designers of AT Protocol clearly had a different vision for what they wanted to achieve.
