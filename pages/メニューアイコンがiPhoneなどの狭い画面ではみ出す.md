---
title: "メニューアイコンがiPhoneなどの狭い画面ではみ出す"
---

from [[Regroup v2 解説]]
メニューアイコンがiPhoneなどの狭い画面ではみ出す
- ![image](https://gyazo.com/75da1e99b5128ffc320d7eb1bfd6cd94/thumb/1000)
    - メニューアイコンがはみ出している
    - TODO: 横幅が小さい時にアイコンを小さくするコードを入れよう

原因
- ボタンの間のスペーサーがiPadに合わせた固定長だったため
- [[CSSで条件分岐と変数と計算を使う]]
- iPadやPCだと広くなりすぎたかもしれない、max-widthを指定すると良いかも？
    - でもいずれもっとボタンを追加したりするだろうから今はいいや


[[pRegroup-done-2019]]
