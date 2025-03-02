---
title: "pytestで一部のテストを除外"
---

サーバ接続を使うテストだけ実行を除外したかった

サーバ接続を使うテストだけデコレータでマークしておく(`mark.server`の`server`は自由に決めて良い)
python

```
@pytest.mark.server
def test_server_io():
	...
```


実行時の-mオプションで実行するマークを指定できるが、これにnotなどの論理演算が使える
`$ pytest -m "not server"`

[[pytest]] [[ソフトウェアテスト]]
