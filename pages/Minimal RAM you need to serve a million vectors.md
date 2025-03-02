---
title: "Minimal RAM you need to serve a million vectors"
---

[[ベクトル検索]]エンジンの要求RAMの話

[Minimal RAM you need to serve a million vectors - Qdrant](https://qdrant.tech/articles/memory-consumption/)
<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>
- 100万ベクトルをメモリ内に保持する場合、[[Qdrant]]には約1.2GBのRAMが必要
- ベクトルをmmapファイルに保存すると、必要なRAMは600MBに減る
- さらにHNSWグラフもmmap保存すると、135MBのRAMで100万ベクトルを提供可能。
- ただし、ディスク性能が検索スピードに大きく影響する。ローカルSSD (IOPS=183k) を使うと、ネットワークストレージ (IOPS=6k) に比べ検索速度が10倍高速化。

[postgresql - How to calculate amount of RAM required for serving X N-dimensional vectors with pgvector (HNSW)? - Stack Overflow](https://stackoverflow.com/questions/77401874/how-to-calculate-amount-of-ram-required-for-serving-x-n-dimensional-vectors-with)
上記のQdrantの記事はベクトルが100次元であると指摘している
