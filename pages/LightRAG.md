---
title: "LightRAG"
---

<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>
LightRAGは「グラフを作って可視化しながらRAGする」を最短で試せる実装です。書籍1冊の可視化にも向きます。以下に、なぜLightRAGが適するか → すぐ動かす手順 → 書籍用の具体ワークフロー → ハマりどころの順でまとめます。

なぜLightRAGが目的に合うか（要点）
- Web UIつきサーバ：文書の取り込み、知識グラフの探索・可視化、簡易RAGクエリがブラウザから実施可能（Ollama互換APIも同梱）。([GitHub](https://github.com/HKUDS/LightRAG))
- 引用（出典）機能：ファイルパス等の出典にひもづけて根拠を辿れる（サーバUI・コア双方の設計に反映）。([GitHub](https://github.com/HKUDS/LightRAG))
- 多形式の取り込み：`textract`経由で PDF / DOC / PPT / CSV / TXT を扱えます。([GitHub](https://github.com/HKUDS/LightRAG))
- ストレージの柔軟性：既定（NetworkX, JSON系）のほか、Neo4jやPostgreSQL＋pgvector/AGE、Milvus/Qdrant/FAISS など実運用向けの構成に拡張可能。([GitHub](https://github.com/HKUDS/LightRAG))
- モデル運用の勘所が明記：抽出には強いLLM（目安 32B級, 長文対応）、埋め込みは `BAAI/bge-m3` や `text-embedding-3-large` を推奨、リランカー有効時はmixモード推奨、等が明示されています。([GitHub](https://github.com/HKUDS/LightRAG))

最短セットアップ（Web UIで触る）
1. インストール（サーバ版）
bash

```
pip install "lightrag-hku[api]"
cp env.example .env
lightrag-server
```

起動後、ブラウザからWeb UIにアクセス（UIで取り込み／グラフ可視化／クエリが可能）。([GitHub](https://github.com/HKUDS/LightRAG))
補足：PyPIの依存関係が自動で入り切らないケース報告あり。`openai`, `transformers`, `ollama`, `nano_vectordb` など必要に応じて追加インストールしてください。([GitHub](https://github.com/HKUDS/LightRAG/issues/333?utm_source=chatgpt.com))
2. .envの主な設定ポイント
    - LLM：OpenAI（APIキー）または Ollama（ローカル）。抽出は強めのモデルを推奨（例：GPT‑4o系、ローカルなら Llama3.1‑70B / Qwen2.5‑32B など）。([GitHub](https://github.com/HKUDS/LightRAG))
    - Embedding：`BAAI/bge-m3` または `text-embedding-3-large`（索引作成と検索で同一モデルを使うことが重要）。([GitHub](https://github.com/HKUDS/LightRAG))
    - Storage：最初は既定（ファイル＋NetworkX）でOK。規模が増えたら Neo4j などへ移行。([GitHub](https://github.com/HKUDS/LightRAG))

書籍1冊を可視化するワークフロー（実務向け）
ゴール：章構造とキーワード／関係をグラフで把握し、クリックで該当ページの根拠へ飛べる状態。

1) 書籍の前処理
- PDFをページ単位でテキスト化（段落単位でも可）。テキストの先頭に `book-title | p.12` のようなページラベルを付けておくと、後でページ出典として引用しやすい。
- そのままWeb UIにドラッグ＆ドロップ、またはAPI/スクリプトで投入。LightRAGはPDF直取り込みも可能（`textract`）。([GitHub](https://github.com/HKUDS/LightRAG))

2) 取り込み（インデクシング）
- Web UIのIndexからアップロード（またはAPI/コア）。
- 取り込みでは エンティティと関係が抽出され、知識グラフとベクタ索引が作られる（抽出品質はLLM依存。強いモデル推奨）。([GitHub](https://github.com/HKUDS/LightRAG))

3) 可視化（Graph）
- Web UIのGraphで、ノード検索・近傍展開・レイアウト切替などが可能。書籍内の人物／概念—関係—章のつながりを俯瞰できる。([GitHub](https://github.com/HKUDS/LightRAG))
- さらに、ストリームリット製のLightRAG GUIでは「挿入・クエリ・可視化・ダウンロード」も可能（必要ならエクスポートしてCytoscape.js等で独自ビューを作る）。([GitHub](https://github.com/HKUDS/LightRAG))

4) 質問（RAGクエリ）
- 書籍の全体像系はglobal/mix、細部はlocalが向く。リランカー有効時はmixが既定推奨。([GitHub](https://github.com/HKUDS/LightRAG))
- 引用（出典）をオンにして、回答とともにどのファイル（ページ）に基づくかを確認。([GitHub](https://github.com/HKUDS/LightRAG))

ページ単位で入れる最小スクリプト（必要なら）
Web UIでも十分ですが、ページ出典を厳密に残したい場合はコアを使ってページごとにIDを振って投入します。
python

```
# 公式の初期化手順に沿う：initialize_storages() と initialize_pipeline_status() が必須
import asyncio, pdfplumber
from lightrag import LightRAG, QueryParam
from lightrag.llm.openai import gpt_4o_mini_complete, openai_embed
from lightrag.kg.shared_storage import initialize_pipeline_status

WORKDIR = "./book_kg"

async def main():
    rag = LightRAG(working_dir=WORKDIR,
                   embedding_func=openai_embed,
                   llm_model_func=gpt_4o_mini_complete)
    await rag.initialize_storages()
    await initialize_pipeline_status()

    texts, ids = [], []
    with pdfplumber.open("book.pdf") as pdf:
        for i, page in enumerate(pdf.pages, start=1):
            txt = page.extract_text() or ""
            texts.append(f"[page={i}]\n{txt}")
            ids.append(f"book#p{i}")  # 後で引用しやすいようページIDを固定
    await rag.ainsert(texts, ids=ids)

    # 例: 全体像のクエリ
    ans = await rag.aquery("この本の中核概念と相互関係を要約して", param=QueryParam(mode="mix"))
    print(ans)

asyncio.run(main())
```

※ 初期化2ステップ（`initialize_storages()` と `initialize_pipeline_status()`）は必須。未実行だとエラーになります。([GitHub](https://github.com/HKUDS/LightRAG))
※ PDFの直接取り込みは `textract` でも可。([GitHub](https://github.com/HKUDS/LightRAG))

推奨設定（日本語書籍を想定）
- Embedding：`BAAI/bge-m3`（多言語） or `text-embedding-3-large`（高精度）を索引・検索で統一。途中で変える場合は該当テーブルやデータディレクトリを再生成。([GitHub](https://github.com/HKUDS/LightRAG))
- LLM（抽出）：強めのモデル（目安 32B級、長文対応）。ローカルなら Llama3.1‑70B / Qwen2.5‑32B を Ollama経由、クラウドなら GPT‑4o系 など。([GitHub](https://github.com/HKUDS/LightRAG))
- Reranker：`BAAI/bge-reranker-v2-m3` などを有効化し、mixモードを既定に。([GitHub](https://github.com/HKUDS/LightRAG))
- Storage：単一書籍は既定で十分。コーパス拡大を見込むなら Neo4j（KG）＋ pgvector（ベクタ）へ段階的に移行。([GitHub](https://github.com/HKUDS/LightRAG))

よくあるハマりどころ
- 依存が自動で入らない：`lightrag-hku` / `lightrag` のPyPI版で不足が出たら、`openai`, `transformers`, `ollama`, `nano_vectordb` などを手で追加。([GitHub](https://github.com/HKUDS/LightRAG/issues/333?utm_source=chatgpt.com))
- Embeddingを途中で変えた：索引作成と検索で同一Embeddingが前提。変更時は関連ベクタテーブル／データを再構築。([GitHub](https://github.com/HKUDS/LightRAG))
- UIのグラフ：Web UIのGraph Viewerは順次改善中のアナウンスあり（機能は提供されています）。([GitHub](https://github.com/HKUDS/LightRAG/issues/685?utm_source=chatgpt.com))

すぐ始めるミニ手順（書籍1冊）
1. `pip install "lightrag-hku[api]"` → `.env` を編集（LLM, Embedding, Storage）→ `lightrag-server`。([GitHub](https://github.com/HKUDS/LightRAG))
2. Web UIのIndexでPDFを投入（または前処理でページ単位にして投入）。([GitHub](https://github.com/HKUDS/LightRAG))
3. Graphタブで主要ノード（概念・人物）を検索→近傍展開→出典リンクでページを確認。([GitHub](https://github.com/HKUDS/LightRAG))
4. mixモードで「この本の背骨」「主要概念の関係」「反対概念は？」などを質問。([GitHub](https://github.com/HKUDS/LightRAG))
5. 必要ならNeo4jやダウンロードで独自の可視化（Cytoscape.js等）に流用。([GitHub](https://github.com/HKUDS/LightRAG))

LightRAGベースで**「書籍→知識グラフ→クリックで根拠」まで一気通貫の雛形をこの場で書き起こせます。対象の本（PDFや章立て）をご提示いただければ、取り込み前処理のひな形とUI操作の最短手順に合わせた運用テンプレ**を作ってお渡しします。
