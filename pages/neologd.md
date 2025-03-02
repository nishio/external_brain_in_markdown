
- いい形態素解析用の辞書
- [neologd/mecab-ipadic-neologd: Neologism dictionary based on the language resources on the Web for mecab-ipadic](https://github.com/neologd/mecab-ipadic-neologd)
- 週2回更新される、cronで自動アップデート可能

`$ brew install mecab mecab-ipadic git curl xz`
`$ git clone --depth 1 https://github.com/neologd/mecab-ipadic-neologd.git`
`$ mecab -d build/mecab-ipadic-2.7.0-20070801-neologd-20180920/`
