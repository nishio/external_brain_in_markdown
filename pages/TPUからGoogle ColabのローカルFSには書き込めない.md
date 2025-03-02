---
title: "TPUからGoogle ColabのローカルFSには書き込めない"
---

from [[日本語BERTのfine-tuning]]
BERTのfine-tuningが少し走って死んだ:

エラーメッセージ: `Unsuccessful TensorSliceReader constructor: Failed to get matching files on /content/gdrive/My Drive/bert-wiki-ja/model.ckpt-1400000: Unimplemented: File system scheme '[local]' not implemented`

[[TPU]]から[[Google Colab]]のローカルFSには書き込めないことが原因
> Local file system is not supported on TPU. You need to use Google Storage.
[https://github.com/google-research/bert/issues/445](https://github.com/google-research/bert/issues/445)

結果の書き出し先として[[GCP Bucket]]が必要
