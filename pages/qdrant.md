
Qdrant - Vector Database
- [https://qdrant.tech/](https://qdrant.tech/)

[Collections - Qdrant](https://qdrant.tech/documentation/concepts/collections/)
> A collection is a named set of points (vectors with a payload) among which you can search. Vectors within the same collection must have the same dimensionality and be compared by a single metric.

[Payload - Qdrant](https://qdrant.tech/documentation/concepts/payload/)
> One of the significant features of Qdrant is the ability to store additional information along with vectors. This information is called payload in Qdrant terminology.
>  Qdrant allows you to store any information that can be represented using JSON.
- プロジェクト名をペイロードに積んでおけば特定のプロジェクトだけから検索したり横断検索したりできそう

[Points - Qdrant](https://qdrant.tech/documentation/concepts/points/)
- IDは64ビット整数、PUTする側が決める
    - UUID的に作るか、連番など他のメカニズムで作るか…
    - 同じIDを指定してPUTすれば上書きされる
    - ペイロードに対する条件を指定して、条件を満たすすべてのIDを取得することができる

[Search - Qdrant](https://qdrant.tech/documentation/concepts/search/)
- 類似度スコアで足切りすることもできるけど、適切な閾値なんてわからないからどちらかというと類似度の可視化の方が良さそう

[Filtering - Qdrant](https://qdrant.tech/documentation/concepts/filtering/)
- "Match Any"
json

```json
{
  "key": "project",
  "match": {
    "any": ["aaa", "bbb"]
  }
}
```

- 全文検索マッチもある
json

```json
{
  "key": "description",
  "match": {
    "text": "good cheap"
  }
}
```

    - インデックスを作らない場合は部分文字列を中に含むかのサーチになる

[Storage - Qdrant](https://qdrant.tech/documentation/concepts/storage/#storage)
- Vector Storage: In-memmory / memmap
- Payload Storage: InMemory / OnDisk
- [[RocksDB]] [RocksDB | A persistent key-value store | RocksDB](https://rocksdb.org/)
- ペイロードが大きいならメモリに載せるのは現実的ではない〜という話
- ミニマムプランで1GB RAMで、このScrapboxのJSONが32MBだから、とりあえず気にせずオンメモリにすべき
    - 裁断スキャンした1000冊の書籍を入れようとするとギリギリあふれるくらい
    - まあまずはスモールスタートだよな

[Indexing - Qdrant](https://qdrant.tech/documentation/concepts/indexing/)
- フルテキストインデックスのトークナイザー、説明を見る限りだと日本語に対してまともに機能するか疑わしい
    - 試してみる
        - [Quickstart - Qdrant](https://qdrant.tech/documentation/quick-start/)
        - [https://gist.github.com/nishio/111f11e078dd68768f5904ea879abe2f](https://gist.github.com/nishio/111f11e078dd68768f5904ea879abe2f)
        - 特に問題なく文字列の部分一致でヒットするな
- インデックスの仕組み
    - > Qdrant currently only uses HNSW as a vector index. HNSW (Hierarchical Navigable Small World Graph) is a graph-based indexing algorithm.
    - [[HNSW]] ([[Hierarchical Navigable Small World Graph]])
        - [[Pinecore]]も同じ仕組み [Hierarchical Navigable Small Worlds (HNSW) | Pinecone](https://www.pinecone.io/learn/hnsw/)
        - [1603.09320 Efficient and robust approximate nearest neighbor search using Hierarchical Navigable Small World graphs](https://arxiv.org/abs/1603.09320)

![image](https://gyazo.com/66730fadc2491f94187fc5054f38d934/thumb/1000)
![image](https://gyazo.com/7fa11a66d9efe8c845339a477292308f/thumb/1000)
![image](https://gyazo.com/edcbeb002bc6bb08531c9ecea269f7f6/thumb/1000)
...
![image](https://gyazo.com/07bee77dd85fdd095bfb55421382d965/thumb/1000)

