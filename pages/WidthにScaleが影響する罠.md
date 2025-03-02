
[[Rect Transform]]のPosにはScaleが影響しないが、WidthにはScaleが影響する
- これに気付いていないと予期せず小さすぎるWidth, Heightを指定してしまう
    - ![image](https://gyazo.com/7b9985546531023cf170b8a4a99ca6c1/thumb/1000)
    - ![image](https://gyazo.com/7a3f200a666ff715451808bc2f2b74a2/thumb/1000)


---以下ログ
![image](https://gyazo.com/8b9f5b38c1364fe1e3714abb486f7453/thumb/1000)
![image](https://gyazo.com/793682c7ca0f056137239a4d97069c5e/thumb/1000)
![image](https://gyazo.com/cc843c01d1dd77c77095389ad28b1981/thumb/1000)
- [[モノリス]]の上端を基準点にして、そこからY方向-1の点にテキストの上端を合わせている

- Widthはいま0だけど、Truncateする場合には適切に(この場合は4とかに)するべき？
    - ![image](https://gyazo.com/fc001ca30c37b1577bdc2a6153ce217d/thumb/1000)
    - Truncateしてないとこうなる
    - と思ったがそもそも水平方向のTruncateはなかった

- > [[Alignment]]の上下方向のボタンを、PowerPointなどの上ぞろえ下ぞろえと混同した。
    - > これは基準点に対してテキストの上端でそろえるか下端でそろえるかという意味なので、アイコン上での表現と逆に「下端でそろえる」をした方がテキストは上に行く。
- と思ったが違うみたい
    - ![image](https://gyazo.com/7b9985546531023cf170b8a4a99ca6c1/thumb/1000)
    - ![image](https://gyazo.com/7a3f200a666ff715451808bc2f2b74a2/thumb/1000)
    - PosにはScaleが影響しないが、WidthにはScaleが影響するみたいだ
        - 今までそれを誤解していて想定より小さく作られていた
        - この状況でなら下ぞろえでモノリス下端に張り付く
        - 縦幅が想定より小さかったために基準点に対するアライメントに見えていた
    - モノリス中心を基準点にしたうえでPosは0でもよい

- WrapとTruncateを設定するとこうなる
    - ![image](https://gyazo.com/620c853d795444ec47fae72b1c5a677b/thumb/1000)

