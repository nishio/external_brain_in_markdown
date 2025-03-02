
- Karabinerの設定ファイルを手で編集したくなかったので生成するプログラムを書いた
    - 2018-08-20 Orz配列を生成
- [[shioシフト]]をKarabiner単独で使いたくなったので設定ファイルによって作り分けるようにした　2020-09-19

設定ファイル
- SIMPLE_KEY_CHAINS.txt
SIMPLE_KEY_CHAINS.txt

```
a u wo vu
```

    - 元キー、シフトなし、左シフト、右シフト
    - ?は空欄
- SPECIAL.txt
    - SIMPLE_KEY_CHAINS.txtでは記号やシフトが絡んだときにやりづらいので記号用のファイルが分かれてる
SPECIAL.txt

```
1LEFT	^slash #はてな
```

    - ^はシフト
- 理想としては[[keylayout]]のデータから生成するのがわかりやすい
    - 作ってみたのでしばらく使ってみる

- リポジトリ [https://github.com/nishio/generate_karabiner_conf](https://github.com/nishio/generate_karabiner_conf)
