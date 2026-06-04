---
title: "LLM WikiをScrapboxスタイルに"
---

初期に作ったLLM Wikiが英語表記の概念/ページタイトルなのことにちょっと摩擦を感じてたんだけど、Scrapbox的スタイルにできるということがわかったので英やと全体をリファクタリングできるか検討してみる

![image](https://gyazo.com/277703830c4e93bcc224ca04fda86195/thumb/1000)![image](https://gyazo.com/254791ffe58c3c5cf821351e9e1bf196/thumb/1000)![image](https://gyazo.com/eaa9e99b6e64a32d11269f8904dc005f/thumb/1000)


![image](https://gyazo.com/d4223184e7338ec835838fe5dbf3b481/thumb/1000)

![image](https://gyazo.com/68f4f623799094574912bbb18db875ab/thumb/1000)

![image](https://gyazo.com/d8e690e02de95d82d44cc6593dc03bf2/thumb/1000)

![image](https://gyazo.com/e60b3c050288be84ed6dfaf94cc752c8/thumb/1000)
- なんかこれ宇宙人と会話しながら対訳辞書を作ってる感じがするな([[プロジェクト・ヘイル・メアリー]]的な)

![image](https://gyazo.com/bd00da8ee74a61deaa76287d58dbc436/thumb/1000)
- 一つ一つ結構難しいが、それぞれに自分がしっくりとくる名前をつけることが将来的にとても有益だと感じる
- 今まではせっかくAIが概念抽出してたのに英語で目が滑ってしっかり自分の中に根を下ろしていなかった

![image](https://gyazo.com/72347c2cd94ad620bcab86aef64a010b/thumb/1000)


真似したい人向けのまとめ
prompt

```
# このwikiのconcepts/ (または主要ページ群) を Scrapbox 流に refactor したい

## 目標
- ファイル名 = Scrapbox 流の自然タイトル (日本語の文タイトル中心 + 定着英語維持)
- 本文中の wikilink を文中スタイル (inline) で配置 — 「## 関連ページ」末尾節依存より優先

## 命名方針

- **A. 元から日本語の概念** → 漢字/ひらがな (例: kabuwake → 株分け)
- **B. 定着した英語 jargon** → 英語維持、スペース区切り (kebab-case 廃止) (例: llm-harness → LLMハーネス)
- **C. 混在自然** → 日英ミックス (例: cost-inversion → 人間と LLM のコスト逆転)
- **強制カタカナ訳禁止** (「コールドスタート面」型の不自然な訳を作らない)
- **ファイル名禁則文字**: `/` `:` `?` `*` `"` `<` `>` `|` `\` (macOS / git で問題)

ユーザは**短い名詞句より文タイトル**を好む。AskUserQuestion で候補を出すときは文タイトル候補を default に入れる。

## workflow (4 phase に分けて atomic commit / 各 phase 後に lint)

### Phase 0: scope 確認
1. 対象 directory を確認 (`concepts/` のみ? `entities/` も含む? `sources/` は date-ID で残す?)
2. wikilink 数 + 影響範囲を計測 (`grep -rohE '\[\[[^]]+\]\]' wiki/ | sort -u | wc -l` 等)
3. 命名方針を user に確認

### Phase 1: mapping draft (一気に決めない、まず案を出す)
1. 対象ファイル全件の `(old basename → new title)` を draft `concept-rename-mapping.md` に書き出し
2. カテゴリ A/B/C で表組み、判断根拠の「メモ」列付き
3. user に**ファイル内で inline 編集してもらう** (大量 Q&A より高速)

### Phase 2: 残り未確定行を対話で確定
- AskUserQuestion で 2-3 候補 + Other (Scrapbox 流文タイトル候補を default に)
- 「概念が混ざってる」flag が来たら**provisional 名 + 切り出し候補メモ**で保留 (split は別 phase)

### Phase 3: scripted 実行
Python script で一括処理 (この順序):
1. `git mv` 各ファイル (**case-only rename は 2-step**: `old.md → old_tmp.md → New.md`)
2. 全 `.md` 内の `[[oldname]]` → `[[newname]]` (alias/anchor 保持: `rf"\[\[{re.escape(old)}(?=[\]|#])"`)
3. 全 `.md` 内の `path/old.md` → `path/new.md` (path ref 置換、log.md や frontmatter `sources:` も含む)
4. `index.md` の `[old](path/new.md)` → `[new](path/new.md)` (display 名揃え)
5. `scripts/lint_wiki.py` の `INDEX_LINK` regex を UTF-8 対応化 (`r"\((?:([^()]*?)/)?([^()/]+)\.md\)"`)
6. `python3 scripts/lint_wiki.py` で broken wikilink: 0 確認

mapping は**長い basename から短い basename へ降順**置換 (prefix collision 回避、例 `kabuwake-implementation` を `kabuwake` より先に処理)。

### Phase 4: file back
今回の経験を `analyses/` ([[concept-split-workflow-20260525]] と同様の形式) に file back。

## 失敗 mode (今回 llm-wiki で hit したもの)

1. **macOS case-insensitive FS**: `ingest → Ingest` のケース変更だけは `git mv` が "target exists" で fail → 2-step rename
2. **wikilink alias の向き**: `[[target|display]]` (target が前、display が後)。逆に書くと lint で broken
3. **prose と wikilink の区別**: 長い identifier (`filing-back-experience`) の prefix を含む短い identifier (`filing-back`) を置換するとき、`(?<![A-Za-z0-9_\-])(filing-back)(?![A-Za-z0-9_\-])` で word boundary を厳密化
4. **lint regex の UTF-8 化**: 多くの wiki で `INDEX_LINK` が ASCII 限定。UTF-8 path を扱う前に regex 更新
5. **`[[log.md]]` のような meta-file への wikilink**: log.md は wikilink target ではないので backtick で `wiki/log.md` と書く

## 期待される副産物

- **「rename = 概念分離 lint」効果**: 命名を決める過程で「単一名で 2 概念扱っていた」page が露見する (llm-wiki では 7 件 flag → 9 新規 concept page 生成、6 split + 1 reframe で成立 86%)
- 用語訂正の機会(`file back`とすべきものが`fill back`となっていた)
- ユーザの命名 preference の articulate 化 (今後の session で再利用可)
```


用語訂正の機会:
- [[fill back→file back]]
