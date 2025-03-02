
![image](https://gyazo.com/25bb95bcf21ce686ff90fc7ccf238e48/thumb/1000)

Ergodoxで親指シフトを実現した
- Windows環境で親指シフトをする場合DvorakJなどのキー書き換えソフトウェアを使うことが一般的
- しかしDvorakJは
    - 打鍵の時間差が一定以内の時に同時打鍵とみなす設計なのでわずかな打鍵の遅れで同時ではないと判定される
    - デフォルトでシフトキーとしてスペース、変換、無変換などが使われていて同時でないと判断されたときの被害が広範
    - おそらくこの設計が原因で `git add -p` が`gi tad d-p`になったり`"abc"`が`"abC’`になったりする
        - アルファベットの後にスペースやシフトが押されたのにアルファベットが遅れて認識されている
- そこでファームウェア書き換え可能なキーボードErgodox EZを用いて親指シフトを実現した
- 記号の配置は仕様通り再現するモチベーションがなかったのでやりたいようにやった
- 意外と記事がないのでここに書いておく

技術的な話
- ソースはここに置いた
    - [https://github.com/nishio/qmk_firmware/tree/thumb_shift/keyboards/ergodox/keymaps/thumb_shift](https://github.com/nishio/qmk_firmware/tree/thumb_shift/keyboards/ergodox/keymaps/thumb_shift)
- 親指シフトのキーとして既存のキーコードを流用するのではなくマクロでシフトキー的挙動を直接実装している
    - なので空打ちしても害はない
    - 修飾キーが2つ増えた状態
- キー定義の大部分がマクロ　[https://github.com/nishio/qmk_firmware/blob/thumb_shift/keyboards/ergodox/keymaps/thumb_shift/keymap.c#L22](https://github.com/nishio/qmk_firmware/blob/thumb_shift/keyboards/ergodox/keymaps/thumb_shift/keymap.c#L22)
- 親指シフトではないが参考になる関連記事 [Ergodoxで親指同時打鍵を実装する](https://qiita.com/derui@github/items/060eebf33716d703b90c)
    - サイズがシビアとのことで心配したが特に何もせずあっさり動いた
    - [彼の実装](https://github.com/derui/qmk_firmware/blob/master/layouts/community/ergodox/derui/hk_util.c#L64)と[僕の実装](https://github.com/nishio/qmk_firmware/blob/thumb_shift/keyboards/ergodox/keymaps/thumb_shift/keymap.c#L81)では1桁サイズが違うかも
- キーコードの列で単純に表現できないものは1文字目KC_NOに続けて非ゼロの時特殊コマンドとして扱っている
    - [https://github.com/nishio/qmk_firmware/blob/thumb_shift/keyboards/ergodox/keymaps/thumb_shift/keymap.c#L144](https://github.com/nishio/qmk_firmware/blob/thumb_shift/keyboards/ergodox/keymaps/thumb_shift/keymap.c#L144)
- まだ英字・記号は実装してない
- 矢印キーを親指シフトで修飾してHomeやPageUpにするのもよさそう