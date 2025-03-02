
[[CID問題]]は[[CMapの再生成]]で解決したが、レアな文字がCIDに置き換わる現象はまだ発生する。
これがそのままだと頻出語が`cid`なんてことになりかねない。

解決策
- 単純に削除
- [[文字ベース言語モデル]]で埋める
- 各書籍ごとに手入力

一冊分を表示してみたが意外と少なかったので手で正解を入力してみた。
python

```
data = data.replace("(cid:12101)", ":")
data = data.replace("(cid:31)", "fi")
data = data.replace("(cid:7743)", "捗")
data = data.replace("(cid:29)", "fl")
data = data.replace("(cid:30)", "ff")
data = data.replace("(cid:13949)", "兎")
data = data.replace("(cid:7656)", "翰")
data = data.replace("(cid:7767)", "灘")
data = data.replace("(cid:12255)", "●")
data = re.sub(r"\(cid:12[678]\d\d\)", "", data)
```

コードと文字の対応が他の出版社でも同じかどうかは疑問。多分違う。
最終行のまとめて潰しているのは、下記のような表示されないCID埋め込みがたくさんあるため。これはきっとPDFが流出した時に誰が流出させたか特定するための電子透かしだろう。
>  エンジニアの知(cid:12705) 的(cid:12710)(cid:12684) 生(cid:12699)(cid:12674) 産(cid:12693)(cid:12755) 術(cid:12696)(cid:12741)(cid:12708)
