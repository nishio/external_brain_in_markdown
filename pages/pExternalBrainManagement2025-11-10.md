---
title: "pExternalBrainManagement2025-11-10"
---

[https://github.com/nishio/external_brain_management](https://github.com/nishio/external_brain_management) つくった
ChatGPT5の全体設計の元、Claude CodeやDevin.aiが今まで作り散らしてきた色々な要素を理解して繋ぎ合わせる

---
あなたは西尾泰和の外部脳(Scrapbox)の内容に、external_brain_in_markdownの中のMarkdownを介してアクセスできる。\
これを知っていると検索が効率的だと思う。\
試しにmemに書かれている`I'm currently programming new translation system using GPT3.5 ChatGPT API, for better translation and custom view using Quartz.`\
がいつ頃描かれたもので、その後どうなったのかについて調べて報告せよ。

<img src='https://scrapbox.io/api/pages/nishio/Claude/icon' alt='Claude.icon' height="19.5"/>
Todos
- ☐ Check git history of mem README.md
    - ここで転けてたので中断した<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
- ☐ Search for GPT3.5/ChatGPT references in external_brain_in_markdown
- ☐ Search for Quartz references in external_brain_in_markdown
- ☐ Analyze timeline and progress
- ☐ Write report


メモ
- リポジトリのどこかにタイムスタンプ付きJSONがあるといいね、各行がいつ書かれたかを知ることができる
- 更新日時やキーワードで絞り込んで検索するツールがあるといいかも
- ベクトル検索もWebサービスではなくローカルで動くようにしてCCに使わせるのがいいかも？

[https://gist.github.com/nishio/4c864a8cb064234421004649bf9eac50](https://gist.github.com/nishio/4c864a8cb064234421004649bf9eac50)
思ったより正しいレポートができている
- memの記述がScrapboxのどこからきているか理解している

---
<img src='https://scrapbox.io/api/pages/nishio/Claude/icon' alt='Claude.icon' height="19.5"/>
memは翻訳システムではなく、日本語Scrapboxのカスタムビューです。
INDEX_FOR_VERCELに書かれていた「GPT3.5翻訳システム」の構想は、memとは別の新しいシステムとして計画されていたものですね。現在のmemは：
- 日本語の /nishio プロジェクトを表示
- カスタムUI（ブレッドクラム、PrevNext、関連ページ表示など）を提供
- Google Translateへのリンクを提供（trans_url）
翻訳版の公開には、別のアプローチが必要ということですね。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
なるほどね。 `https://mem.nhiro.org/ja/<page>` で external_brain_in_markdown のデータを取得してレンダリングするようにできる？で、英訳は`https://mem.nhiro.org/en/<page>` にする


CLAUDE.mdのデータフロー概要
_

```
Scrapbox (nishio, nishio-en)
    ↓
[from_scrapbox] データ取得・変換
    ↓
[external_brain_in_markdown] Markdown保存

[etude-github-actions] 翻訳パイプライン
    ↓
[mem] Web表示 (mem.nhiro.org)
```

これ若干正しくなくて、nishio→etude-github-actions→nishio-en と nishio→memだね
そしていま新しいフローをつけつつある
etude-github-actionsの翻訳パイプラインは低品質だが、全てのページが一応訳されているのでベースラインとしてまずはそれで進めよう、将来的にはより高品質なものでオーバーライドできると良い


人間が使うUIとしてCosense(Scrapbox)は有能なのだが、「人間とAIが共同作業する」となったらGitHub上のMarkdownが有力になってくる
- なのでCosense(Scrapbox)は「人間がデータを吐き出す場」であり、それをMarkdownにしてGitHubにいれてる`external_brain_in_markdown`が人間由来データのストレージ、AIが作成するものもGitHubに(混ざらないようにfolderわけするなどして)入れるのが良さそう

やべ、AIさんがなんかややこしくしてきたw
- ![image](https://gyazo.com/af810403dfd874b9125f1c2c6c34f0a2/thumb/1000)

ローカル環境ではシンボリックリンクを使い、Vercelではprebuildでgit cloneする実装にした
- すごく時間がかかるようになるのではと思ったが1m30くらいでビルドできるな、ほんとか？

作業日記
- [https://github.com/nishio/external_brain_management/blob/main/docs/diary/2025-11-11.md](https://github.com/nishio/external_brain_management/blob/main/docs/diary/2025-11-11.md)

next: [[pExternalBrainManagement2025-11-11]]
