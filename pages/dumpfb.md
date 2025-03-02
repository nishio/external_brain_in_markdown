
昔Facebookのアクティビティログをファイルに書き出すために作ったもの
- [https://github.com/nishio/dumpfb](https://github.com/nishio/dumpfb)
- 2018−10−20 node-webkitが古かったのでpure browserで動くように書き換えた
    - しかしDOMをどんどん削ってファイルに吐いてた従来バージョンと違って、どうしてもDOMにどんどん積んでいくことになるので重たい。
    - 今だったら[[Puppeteer]]を使うかな…
