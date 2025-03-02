
- [[Markdown]]で書いて出版できるプラットフォーム
- GithubやBitbucketと連携できる
- Githubにpushしたら自動でプレビュー作成
    - Dropbox連携でシステム側が作成したファイル(PDF, MOBI, EPUB)が共有される
- チュートリアルに従うだけで1ポモドーロくらいでそこまで設定できる
- 目次は自動で生成される
- こういうページも生成される
    - ![image](https://gyazo.com/bc13bcb02227c14f023851e1f6aeb40d/thumb/1000)

- Leanpub Flavored Markdown
    - [https://leanpub.com/help/manual](https://leanpub.com/help/manual)
    - 技術書を書くときに足りないところが拡張されたMarkdownになっている
- タイトルとシンタックスハイライト付きのコードリージョン
:

```
{title="Displays 'true!' since 0 is true in Ruby", lang=ruby}
~~~~~~~
if 0 then
  ...
end
~~~~~~~
```

![image](https://gyazo.com/e9b5656671c287eab658f4dd1cd9ee2c/thumb/1000)

- 脚注
:

```
Aaaa[^foo].

[^foo]: footnote
    and second line of footnote
```

文中にはこうリンクの形で入る
- ![image](https://gyazo.com/1f35fb6f5d6ed7e2536ff2bf5e5334c5/thumb/1000)
実際の脚注は全部の最後にNotesって章が作られてそこにまとめられている(それを脚注と言うのか？)
![image](https://gyazo.com/ea1e8a371846e630e65cccce99c6f3de/thumb/1000)
Notesの中の各文章には元の場所にジャンプするリンクが付与されている
![image](https://gyazo.com/84db800d9ad55ddee756ca4d50cccebe/thumb/1000)
PDF版だと脚注としてページ下部に表示されるようだ。日本語が化けてるけど、多分僕が書籍を英語版の設定にしているせいでフォントが埋め込まれてないのかな？
![image](https://gyazo.com/8dbcfc17dcaa5811bab894cc2d1b3f88/thumb/1000)
- [https://leanpub.com/help/manual#leanpub-auto-switching-back-and-forth-between-language-fonts](https://leanpub.com/help/manual#leanpub-auto-switching-back-and-forth-between-language-fonts)
- 日本語フォントを使うことを指示する命令がある

- 画像
    - `![An awesome sword](images/Sword.png)`

#電子書籍
