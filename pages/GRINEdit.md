---
title: "GRINEdit"
---

<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>
見つかりました。GRINEdit のソースコードZIPは SourceForge 上の `alpha0.10-src.zip` として公開されています。
確認できた構成はこうです。
`alpha-0.10` には、バイナリと思われる `GRINEdit-alpha0.10.zip` と、ソースと思われる `alpha0.10-src.zip` が並んでおり、どちらも 2006-06-09 付けです。`alpha0.10-src.zip` は 3.0 MB と表示されています。([SourceForge](https://sourceforge.net/projects/grinedit/files/grinedit/alpha-0.10/)) SourceForge のダウンロードページでも `alpha0.10-src.zip` というファイル名が確認できます。([SourceForge](https://sourceforge.net/projects/grinedit/files/grinedit/alpha-0.10/alpha0.10-src.zip/download))
取得するなら、おそらくこれでいけます。
bash

```
curl -L -o alpha0.10-src.zip \
  "https://sourceforge.net/projects/grinedit/files/grinedit/alpha-0.10/alpha0.10-src.zip/download"

unzip -l alpha0.10-src.zip | head -50
```

一方で、`alpha-0.20` 側には `grinedit-bin-rev187-20061128162223.zip` だけがあり、SourceForge の一覧上ではソースZIPは見当たりません。([SourceForge](https://sourceforge.net/projects/grinedit/files/grinedit/alpha-0.20/)) さらに JAIST の SourceForge.jp ミラーには `rel-visualizer` 配下に 2006〜2007年頃のリリースディレクトリが残っており、`23582/` には `grinedit-bin-rev194-20070115173728.zip` という、より新しそうなバイナリもありますが、そこにもソースZIPは表示されていません。([JAIST FTP](https://ftp.jaist.ac.jp/pub/sourceforge.jp/rel-visualizer/)) ([JAIST FTP](https://ftp.jaist.ac.jp/pub/sourceforge.jp/rel-visualizer/23582/))
現時点の見立ては、公開状態で確実に見つかるソースは `alpha0.10-src.zip`、より新しい rev187 / rev194 のソースは今回の検索範囲では未発見です。次に掘るなら、`alpha0.10-src.zip` の中身を展開してパッケージ名・ビルド方式・リポジトリ痕跡を調べるのがよさそうです。
