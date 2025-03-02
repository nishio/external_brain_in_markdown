
公式に実装された

このページはそれができる前のメモ
2019-03-25
Scrapboxを[[横断検索]]したい
- 公開の場所に置くことができないが、検索対象にしたいものがチラホラある
- 自分のプロジェクトを検索する際についでに他人のプロジェクトも検索できたら良いかも

2019-05-15 [https://twitter.com/shiology/status/1128228164121927680](https://twitter.com/shiology/status/1128228164121927680)
- Chrome拡張を入れた
- ![image](https://gyazo.com/2be9ed43b6059731a692a28f5396fd3b/thumb/1000)
- 便利


---
案1:
- `https://scrapbox.io/<project_name>/search/page?q=test`
- をiframeで複数ひらけばいいんじゃなかろうか
- [[ちょこっとサービス]]の仕組みを使ってはどうか。
- 結果:
    - Scrapboxがレスポンスヘッダに `X-Frame-Options: SAMEORIGIN` をつけてくるので同一オリジン内からしか開けない
    - →UserScriptかChrome拡張で実現するしかない

案2:
- UserScriptで実現できるか
- 一応JS経由で複数のプロジェクトの検索結果ページを埋め込むことはできた
- ![image](https://gyazo.com/67531165ff2f68bda039f28df59db46f/thumb/1000)
- スクリプト: [[nishio#5c984440aff09e00003f0141]]
    - ページ名が[[cross_search]]の時だけ発動
    - URLに"?キーワード"とつけるとそのキーワードで検索

