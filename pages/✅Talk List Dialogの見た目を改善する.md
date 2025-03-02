---
title: "✅Talk List Dialogの見た目を改善する"
---

from [[✅ダイアログの見た目を改善する]]
Talk List Dialogの見た目を改善する

after
- ![image](https://gyazo.com/de44ba66120e18f25139076911555b8e/thumb/1000)

before
- ![image](https://gyazo.com/6047f8b775caaac14548d4269dbbd426/thumb/1000)
    - 考えたこと
        - リスト冒頭のマージンが無駄
        - タイトルをリンクにしたらShowLogボタンは不要？
            - でも暗黙の操作より明示的な操作の方がわかりやすい？
        - タイトル手前で改行すると頭が揃ってみやすそう
        - アイテムの間にマージンつける
- [React List component - Material-UI](https://material-ui.com/components/lists/)
    - ![image](https://gyazo.com/03b898f38898492d41187a402811254e/thumb/1000)
        - 開発用PCでは使ってないからデータがしょぼいな
    - ![image](https://gyazo.com/e75003e48602dd888f884998222b72ce/thumb/1000)
        - 一時的にそれっぽいタイトルを表示するようにしてみた
- iPhone Xサイズにしてみる
    - ![image](https://gyazo.com/7a9ed73db37187fa97135422b7c8468f/thumb/1000)
        - うーん、ボタンが縮んでテキストがはみ出てるのは微妙だなぁ
    - ボタンをdivで囲んだパターン
        - ![image](https://gyazo.com/1d2e04258b1debdabaf7600c787dad62/thumb/1000)
    - ListItemの外に出したパターン
        - ![image](https://gyazo.com/7ef8149fcd704898eb5abafb14994b6a/thumb/1000)
    - 前者がいい
- ボタンが縮むのは親にflexがついてるから
- ボタンにalign-items: flex-end;して下に揃えた
- ![image](https://gyazo.com/ae01e39e383ecb4621a638308abf68e2/thumb/1000)

- 実機で確認
    - ![image](https://gyazo.com/0771827811547cdaf231128ea8e29856/thumb/1000)
        - あー、テキストの長さがまちまちだとそうなるのかー
- スマホのローカルストレージに保存されてるトークリストを開発PCに持ってきて試したい
- [[✅トークリストのエクスポート/インポート]]
- 開発PCで再現できた
    - ![image](https://gyazo.com/3f100bfa6f94e76c94c4a94872e931c2/thumb/1000)
- スペース節約のためにボタンが1列になれるならなった方がいいと考えてたけどそれほど良くないな
    - ![image](https://gyazo.com/9be9d3c4d133665f3631747ba425bbce/thumb/1000)
- `flex-basis: 110px;`で基本サイズを大きいボタンの幅にする、これで基本は折り返しになる
- `flex-grow: 1;`をテキストとボタンの両方のdivにつける、これでテキストが短い時にはボタンのdivも引き伸ばされ、十分伸びたら1列になる
- `text-align: right;`でボタンを右揃えにしておく。ボタンのdivがどうなろうが右端が揃うようになる。
- ボタンがテキストより上に突き出すのはダサい
    - ![image](https://gyazo.com/6275055b1929fe2c402324a572658b9e/thumb/1000)
    - `align-self: flex-start;`と`align-self: flex-end;`でテキストを上に、ボタンを下にする
- リストの領域に薄墨を引いてボタン同様のシャドウをつける
    - `background: #eee;`
    - `box-shadow: 0px 3px 1px -2px rgb(0 0 0 / 20%), 0px 2px 2px 0px rgb(0 0 0 / 14%), 0px 1px 5px 0px rgb(0 0 0 / 12%);`
- できた
    - ![image](https://gyazo.com/de44ba66120e18f25139076911555b8e/thumb/1000)

divの状態
![image](https://gyazo.com/af8183485a244dd14a681f7903fca9b2/thumb/1000)![image](https://gyazo.com/ff97de0ed8a2b17a144622b1f7179974/thumb/1000)

