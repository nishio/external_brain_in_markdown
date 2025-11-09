---
title: "Embedding Atlas(Apple)"
---

[Overview | Embedding Atlas](https://apple.github.io/embedding-atlas/overview.html)

> [NirantK](https://x.com/NirantK/status/1954081728525742365) [[Apple]] just dropped a killer open-source [[visualization tool for embeddings]] — [[Embedding Atlas]] — and it’s surprisingly powerful for anyone working with large text+metadata datasets.
>  Apple は、埋め込み用のキラーなオープンソース視覚化ツールである Embedding Atlas をリリースしたばかりですが、これは大規模なテキスト + メタデータ データセットを扱う人にとって驚くほど強力です。
>
>  This reminds me of [[Nomic]]'s Atlas, but I never got around to using it
>  これは Nomic の Atlas を思い出させますが、私はそれ  を使う暇がありませんでした
>
>  We’re talking real-time search, multi-million point rendering, and automatic clustering with labels.
>  リアルタイム検索、数百万ポイントのレンダリング、ラベルによる自動クラスタリングについて話しています。
>
>  One of their showcase examples visualizes ~200K wine reviews using embeddings + metadata like price, country, and tasting notes. And it is lightning fast even on my browser! No separate code needed!
>  彼らのショーケースの例の 1 つは、埋め込み + メタデータ(価格、国、テイスティング ノートなど)を使用して、~200K のワイン レビューを視覚化します。そして、私のブラウザでも超高速です!別途コードは不要です!
>
>  It nails what most LLM devs need but often hack together:
>  これは、ほとんどの LLM 開発者が必要としているものを釘付けにしていますが、多くの場合、一緒にハッキングします。
>
>   [[UMAP]] projections
>   Faceted search across metadata (e.g. “country vs. price”)
>   Hover + tooltip on raw points
>   Interactive filters, histograms, and cluster overlays
>   Cross-linked scatterplot + table views
>   UMAP 投影法
>   メタデータ全体での  ファセット検索(例:「国と価格」)
>   生のポイントに  カーソルを合わせる + ツールチップ
>   対話型フィルター、ヒストグラム、クラスターオーバーレイ
>   架橋散布図 + テーブルビュー
>
>  Under the hood:
>  • Fast rendering using WebGPU (with WebGL fallback)
>  • Embedding-based semantic similarity search
>  • Kernel density contours for spotting clusters or outliers
>  ボンネットの下:
>  • [[WebGPU]] を使用した高速レンダリング ([[WebGL]] フォールバックあり)
>  • 埋め込みベースのセマンティック類似性検索
>  • クラスターまたは外れ値を検出するためのカーネル密度等高線
>
>  You just upload your .jsonl or .csv with text + vector + metadata. It handles the rest: clustering, labeling, UI layout, everything.
>  テキスト+ベクター+メタデータを含む.jsonlまたは.csvをアップロードするだけです。クラスタリング、ラベル付け、UIレイアウトなど、残りをすべて処理します。
>
>  This feels like the LLM-native version of Tableau — but optimized for text, chat and modern data needs
>  これは Tableau の LLM ネイティブ バージョンのように感じられますが、テキスト、チャット、最新のデータのニーズに合わせて最適化されています
>
>  If you’re building RAG evals, search tuning, clustering explainability, or even dataset audits — this could be your new favorite tool.
>  RAG 評価、検索チューニング、クラスタリングの説明可能性、さらにはデータセット監査を構築している場合、これは新しいお気に入りのツールになる可能性があります。
>  ![image](https://pbs.twimg.com/media/Gx5K-KbbsAIO95H?format=jpg&name=medium#.png) ![image](https://pbs.twimg.com/media/Gx5K-f-akAAUZRM?format=jpg&name=medium#.png)

