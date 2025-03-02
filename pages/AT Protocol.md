---
title: "AT Protocol"
---

[Protocol Overview | AT Protocol](https://atproto.com/guides/overview)

[[AT ProtocolのLexicon]]

[Identity | AT Protocol](https://atproto.com/guides/identity)
ATプロトコルでは、各ユーザーは、alice.host.comやalice.comのようなドメイン名ハンドルと、ホスト間での移行を可能にする一貫した "[[DID]]"([[分散型ID]]) を持つ。
- ID管理：ユーザーは安定したグローバルIDを作成し、公開鍵を安全に配布する。IDは移植可能で、キーのローテーションも可能。
- 識別子：ハンドルとDIDの2種類の識別子を使用。ハンドルはDNS名、DIDは安全で安定したIDとして機能。
- ハンドル解決：atprotoのハンドルは、ユーザーの署名公開鍵とホスティングサービスを含むDIDドキュメントへと解決するDIDに解決する。
![image](https://gyazo.com/a21869f3aa6d3ac4b9394fc64c5d5f3f/thumb/1000)
- [[Hosting Provider]]
