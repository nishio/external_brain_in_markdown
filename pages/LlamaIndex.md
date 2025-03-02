---
title: "LlamaIndex"
---

雑な解説:
- GPT3に、学習時に使われていないデータを参考資料としてプロンプトに含めることで
    - 学習時に存在しなかった最新の情報
    - 電子書籍などの著作権的にインターネット上でアクセス可能にできないデータ
    - グループウェアの中の顧客コンタクト履歴のデータなど社外に公開できないもの
- 〜などをGPT3が使うことができるようになる仕組み
- 典型的な利用法:
    - 手元の文書からOpenAI APIで[[埋め込みベクトル]]を作る
    - クエリー文章に対して、関連のある文書を[[ベクトル検索]]で見つける
    - その文書をGPT3へのプロンプトに埋め込む

repo: [GitHub - jerryjliu/gpt_index: LlamaIndex (GPT Index) is a project that provides a central interface to connect your LLM's with external data.](https://github.com/jerryjliu/gpt_index)
docs: [Welcome to LlamaIndex 🦙 (GPT Index)! — LlamaIndex documentation](https://gpt-index.readthedocs.io/en/latest/index.html)
3rd party blog: [LlamaIndex クイックスタートガイド｜npaka｜note](https://note.com/npaka/n/n8c3867a55837)

old name: [[GPT-Index]]
