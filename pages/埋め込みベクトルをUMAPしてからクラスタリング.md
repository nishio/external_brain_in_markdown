---
title: "埋め込みベクトルをUMAPしてからクラスタリング"
---

[[埋め込みベクトル]]を[[UMAP]]してから[[クラスタリング]]
<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>
1) テキストでの実証
- 文書クラスタリングの体系的比較（NEJLT 2023）
    - [[An Empirical Configuration Study of a Common Document Clustering Pipeline]]
    - BERT 埋め込み＋次元削減（UMAP/PCA）＋クラスタリング（k‑means/HDBSCAN）のパイプラインを複数データセット（SNACK/AG News/Reuters）で比較。
    - 結果として 「bert_umap_hdbscan」または「bert_umap_kmeans」が最良であることが多い。次元数は 10–15 次元で性能が頭打ちになりやすく、2D など極端な低次元は不利。時間面では UMAP の計算コストは `n_neighbors` に強く依存（20→数秒、1280→数百秒）という計測も示されています。
    - 2次元に落とすのは明らかに悪い<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
- [[UMAP]] のドキュメント：文書埋め込みチュートリアル
    - 20 Newsgroups（ラベル付きテキスト）を題材に、テキスト埋め込み→UMAP→HDBSCAN の流れが紹介され、同一話題の文書が近傍にまとまることを確認。([umap-learn.readthedocs.io](https://umap-learn.readthedocs.io/en/latest/document_embedding.html?utm_source=chatgpt.com))
    - これは埋め込みベクトルではなく[[TfidfVectorizer]]だね<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
- [[BERTopic]]/[[Top2Vec]] 系の設計意図
    - BERTopic は 「埋め込み→UMAP→HDBSCAN→c‑TF‑IDF」 を前提としており、Top2Vec でも 「UMAP で低次元化→HDBSCAN で高密度領域を検出」を中核に据え、さらにトピックベクトルは元の高次元空間で計算して UMAP の歪みを補っています（「UMAP+HDBSCAN は“ラベル付け工程”で、トピックの代表ベクトル計算は原空間で行う」）。([maartengr.github.io](https://maartengr.github.io/BERTopic/getting_started/dim_reduction/dim_reduction.html?utm_source=chatgpt.com))
- 次元削減そのものの妥当性（テキスト）
    - LREC 2024 の評価研究では、文埋め込みの PCA による 50% 程度の次元削減で性能劣化は小さく、むしろ改善するケースもあると報告。非線形の UMAP に限定しなくても、**“高次元のまま”より“適度に落とす”**が理にかなう状況が多いことを示します。([ACL Anthology](https://aclanthology.org/2024.lrec-main.579.pdf?utm_source=chatgpt.com))
    - これはたかだか50%しか削減していないので「2次元に落とした時にどうなるか」とは無関係<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>



2) なぜテキストでも効くのか（幾何の観点）
- コサイン幾何と近傍保存
    - 文埋め込みは L2 正規化して コサイン距離で扱うのが通例。UMAP は任意の距離（`metric='cosine'` など）で近傍グラフを構築でき、近傍構造を保ったまま低次元へ写像します。こうして得た座標に対して Euclid 距離で k‑means/HDBSCAN を動かすのが一般的な設計です。([umap-learn.readthedocs.io](https://umap-learn.readthedocs.io/en/latest/document_embedding.html?utm_source=chatgpt.com))
- BERT 系の“異方性（anisotropy）”
    - 文埋め込み空間は狭い錐体に集中しがち＝距離が判別力を失いやすい。正規化やホワイトニングなどの前処理で幾何を整えるとクラスタの分離が改善するという報告があります。UMAP 前処理と相性がよい理由の一つです。([ACL Anthology](https://aclanthology.org/D19-1006/?utm_source=chatgpt.com))


3) ただし：UMAP 前処理の注意点
- 密度は完全には保存されない → HDBSCAN の判断が変わり得る
    - UMAP は“近傍”は保ちますが密度は歪みやすいため、HDBSCAN が過分割/過結合することがあります。UMAP 公式も「クラスターリングの前処理として使うのは有効だが、議論があるので慎重に」と明記。([umap-learn.readthedocs.io](https://umap-learn.readthedocs.io/en/latest/clustering.html?utm_source=chatgpt.com))
- 再現性（ランダム性・データ順序依存）
    - UMAP は確率的。`random_state` 固定で再現性は上げられますが、完全ではなく、入力順や並列化でも差が出ることがあります（BERTopic FAQ/UMAP の再現性解説や Issue）。([umap-learn.readthedocs.io](https://umap-learn.readthedocs.io/en/latest/reproducibility.html?utm_source=chatgpt.com))
- 計算コスト
    - `n_neighbors` を上げると UMAP の計算時間は急増します（実測図あり）。10–15 次元あたりで止めるのが妥当という実験知見もあります。

4) 実務での指針（テキスト埋め込み想定）
A. 並走ベースライン（まずは両方試す）
1. 直クラスタリング：HDBSCAN（`metric='cosine'`）を元の埋め込みに直接。
2. 線形削減：PCA で 50–200 次元に落としてから HDBSCAN/k‑means。
3. UMAP 削減：UMAP（`metric='cosine'`、`n_components=10–15`、`min_dist∈[0,0.3]`、`n_neighbors=15–50` を起点）→ HDBSCAN/k‑means。
比較は ARI/AMI（ラベルあり）や シルエット/DBI＋トピックコヒーレンス（c_v など）＋**安定性（ブートストラップでの再学習一致度）**で。
B. ハイパラの初期値
- UMAP：`metric='cosine'`、`n_components=10–15`、`n_neighbors≈20` は教科書的な初期点。`n_neighbors` は大きくすると計算が重くなります。
- HDBSCAN：`min_cluster_size` は「最小でもこのくらいは一まとまりであってほしい」サイズに。必要なら `soft_clustering`（確率出力）で全点に割当ても可。([hdbscan.readthedocs.io](https://hdbscan.readthedocs.io/en/latest/basic_hdbscan.html))
C. いつ UMAP を避ける/控えるか
- クラスタ境界の安定性が最優先（監査性が重要）
- 密度の歪みが致命的（例：出現頻度の差をそのまま密度として扱いたい）→ densMAP などの密度保存版を検討。([umap-learn.readthedocs.io](https://umap-learn.readthedocs.io/en/latest/densmap_demo.html?utm_source=chatgpt.com))
- データが小規模で、元々の次元（例：384/768 次元）でも HDBSCAN が十分動く場合。
- まずは PCA ベースの軽量系で十分な時。([ACL Anthology](https://aclanthology.org/2024.lrec-main.579.pdf?utm_source=chatgpt.com))
D. UMAP を使うなら
- 乱択の影響を抑える：`random_state` を固定、同一条件で数回走らせ一致率を見る。([umap-learn.readthedocs.io](https://umap-learn.readthedocs.io/en/latest/reproducibility.html?utm_source=chatgpt.com))
- L2 正規化（少なくとも UMAP 後）を入れると安定しやすいという報告。
- Top2Vec に倣い、ラベル付けは UMAP 空間、代表ベクトルやセンチロイドの計算は原空間という使い分けも有効。([ar5iv](https://ar5iv.labs.arxiv.org/html/2008.09470?utm_source=chatgpt.com))

まとめ
- 画像だけでなく、テキスト埋め込みでも UMAP 前処理は（適切な次元・パラメータなら）品質・計算の両面で利があることが複数研究・実装系で示されています。特に 10–15 次元程度に落としてから HDBSCAN/k‑means は強い構成です。
- 一方で、密度歪み・再現性というトレードオフがあるため、UMAP なし/PCA ありのベースラインと並走し、外的指標（ARI/AMI）・内的指標・トピックコヒーレンス・安定性で選ぶのが安全です。([umap-learn.readthedocs.io](https://umap-learn.readthedocs.io/en/latest/clustering.html?utm_source=chatgpt.com))
必要なら、手元のコーパスに対して上記 A–D をそのまま回せる**最小実験計画（指標＋推奨ハイパラの表＆コード断片）**を用意します。
