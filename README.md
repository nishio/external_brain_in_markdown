# external_brain_in_markdown

Scrapbox プロジェクト [nishio](https://scrapbox.io/nishio/) のページを Markdown として保存するデータリポジトリです。

このリポジトリの本文データは GitHub Actions によって自動生成されます。変換コードは別リポジトリ [nishio/from_scrapbox](https://github.com/nishio/from_scrapbox) で管理しています。

## 内容

- `pages/`: Scrapbox の各ページを Markdown ファイルとして保存したもの
- `.github/workflows/update_markdown.yml`: Scrapbox から `pages/` を更新する workflow
- `README.md`: このリポジトリの説明

## 更新方法

通常は毎日 JST 05:00 に GitHub Actions の `Update Markdown Files` workflow が実行されます。

workflow は次の処理を行います。

1. このデータリポジトリを checkout する
2. [nishio/from_scrapbox](https://github.com/nishio/from_scrapbox) を `_tools/from_scrapbox` に checkout する
3. Scrapbox の `/nishio` を export する
4. export した JSON を Markdown に変換する
5. `pages/` を生成結果と同期し、差分があれば commit する

手動で更新する場合は、GitHub Actions の `Update Markdown Files` から `Run workflow` を実行します。

## 注意

- `pages/` は生成物です。手作業で編集しても、次回更新時に上書きまたは削除される可能性があります。
- Scrapbox export には repository secret `SID` が必要です。
- 変換処理を変更する場合は、このリポジトリではなく [nishio/from_scrapbox](https://github.com/nishio/from_scrapbox) を変更します。
