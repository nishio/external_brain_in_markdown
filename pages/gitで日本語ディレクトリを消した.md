---
title: "gitで日本語ディレクトリを消した"
---

- ローカルで消したけどstagingされてない状態でstagingすることができなくてジタバタしてしまった
- `$ git checkout .`
    - まず綺麗な状態に戻した
- `$ git rm -r "日本語ファイル名"`
    - zshの選択肢補完で選択した後、ディレクトリ名を引用符で括った
- これで無事消せた
