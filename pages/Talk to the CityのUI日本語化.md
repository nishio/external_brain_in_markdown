---
title: "Talk to the CityのUI日本語化"
---

[[Talk to the City]]はUIが基本は英語で、他の言語に関してはコンテンツと一緒にGPT3.5で翻訳してる
ソースコードにこんな感じで書いてあり、設定ファイルの言語の指定を見て翻訳する
translation.py

```
UI_copy = ["Argument", "Original comment", "Representative arguments",
           "Open full-screen map", "Back to report", "Hide labels", "Show labels",
           "Show filters", "Hide filters", "Min. votes", "Consensus",
           "Showing", "arguments", "Reset zoom", "Click anywhere on the map to close this",
           "Click on the dot for details",
           "agree", "disagree", "Language", "English", "arguments", "of total",
           "Overview", "Cluster analysis", "Representative comments", "Introduction",
           "Clusters", "Appendix", "This report was generated using an AI pipeline that consists of the following steps",
           "Step", "extraction", "show code", "hide code", "show prompt", "hide prompt", "embedding",
           "clustering", "labelling", "takeaways", "overview"]
```


この方法は翻訳データを用意しなくても、どんな言語でも設定ファイルに書くだけで翻訳できるので、素晴らしい手抜き多言語対応だと思う(褒めてる)
しかし日本語話者が多数派で、英語アレルギーの人もいる状況だと、デフォルトで英語画面で「日本語にも切り替えられるよ！」って言っても切り替えずに離脱しちゃうんじゃないかなぁ

というわけで「日本語デフォルト」にしたい
「日本語単一」と「日本語デフォルト、切り替えあり」だと前者の方が楽そうだし、今回のニーズにはとりあえず前者で良さそうなのでそれでやる

とりあえず英日のデータは作った
:

```
{'Argument': '議論',
 'Original comment': '元のコメント',
 'Representative arguments': '代表的な議論',
 'Open full-screen map': '全画面地図を開く',
 'Back to report': 'レポートに戻る',
 'Hide labels': 'ラベルを非表示にする',
 'Show labels': 'ラベルを表示',
 'Show filters': 'フィルターを表示',
 'Hide filters': 'フィルターを非表示',
 'Min. votes': '最小投票数',
 'Consensus': 'コンセンサス',
 'Showing': '表示中',
 'arguments': '議論',
 'Reset zoom': 'ズームをリセット',
 'Click anywhere on the map to close this': 'このメッセージを閉じるには地図のどこかをクリックしてください',
 'Click on the dot for details': '詳細を見るには点をクリックしてください',
 'agree': '同意する',
 'disagree': '同意しない',
 'Language': '言語',
 'English': '英語',
 'of total': '合計',
 'Overview': '概要',
 'Cluster analysis': 'クラスター分析',
 'Representative comments': '代表的なコメント',
 'Introduction': '導入',
 'Clusters': 'クラスター',
 'Appendix': '付録',
 'This report was generated using an AI pipeline that consists of the following steps': 'このレポートは、以下のステップで構成されるAIパイプラインを使用して生成されました',
 'Step': 'ステップ',
 'extraction': '抽出',
 'show code': 'コードを表示',
 'hide code': 'コードを非表示',
 'show prompt': 'プロンプトを表示',
 'hide prompt': 'プロンプトを非表示',
 'embedding': '埋め込み',
 'clustering': 'クラスタリング',
 'labelling': 'ラベリング',
 'takeaways': 'まとめ',
 'overview': '概要'}
```


翻訳はuseTranslatorAndReplacementsが返してくる関数`t`で`{t("Representative comments")}`みたいな感じにしている
このtの中で上記をハードコードしたらいいんじゃないかな
実際のコードはuseMemoとか使ってるけど、それって全データを翻訳する時に重たいからだと思う、この程度だったらシンプルに書いていいんじゃないかな？

続きはまた今度
