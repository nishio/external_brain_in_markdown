
- 1つのindex.htmlでできているようなアプリ(SPA)で、パラメータを渡したい時がある
- パスに入れるとindex.htmlではないファイルにアクセスしにいってしまう
    - 設定で回避できるが面倒だな、とおもってハッシュやクエリパラメータを使ってた
- [[Netlify]]だとその設定は、プロジェクトのルートのnetlify.tomlに4行書くだけ
netlify.toml

```toml
[[redirects]]
  from = "/*"
  to = "/index.html"
  status = 200
```


- 「buildに_redirectを置くwebpackの設定を書いて…」とやってる人がいたけど必要ない
- [[Add to Home screen]]
