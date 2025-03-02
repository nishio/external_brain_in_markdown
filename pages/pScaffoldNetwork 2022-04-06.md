
[[pScaffoldNetwork]]
書籍からの[[足場ネットワーク]]作成、できた
- 書籍などのようにページにタイトルがついていない場合、コンテンツページを上にするより、表記揺れ解消ページを上にする方が面白そう
    - ![image](https://gyazo.com/3433781e56ea22b09dc6c192aa7c685b/thumb/1000)
    - ![image](https://gyazo.com/716235f54a965d1ef2914dd1c5e98051/thumb/1000)

:

```
:len(docs) 223
:all body length 144072
:average body length 646.0627802690583
convert to tokens 0.416135923
 construct SA 0.12402529000000001
height_to_group 0.09916798400000015
filter groups 0.020757480999999967
:len(list(groups)) 2004
calc score / per page grouping 0.0030685299999999582
select good links 0.021269355000000045
:len(selected_links 987
generate variant pages / make links 0.019899406999999814
output 0.031460328999999954
python3 scaffold_network.py  1.13s user 0.10s system 97% cpu 1.260 total
```


14万文字(223文書、平均646文字)を入力として形態素解析と接尾辞配列の作成に0.6秒くらい
ドキュメント間の曖昧一致部分列を全部ピックアップして1文書にしか出現しないものを捨てて2000件のリンク候補を抽出する、ここが0.1秒
リンク候補にスコアをつけてページごとにまとめて上位数件を選んで1000件程度にする、ここが0.02秒
Scrapbox用のJSONを生成するのに0.05秒

細々とステップ分けたけどこの程度の規模だと爆速で、全部こみで1.1秒しかかからない

:

```
:len(docs) 425
:all body length 311207
:average body length 732.2517647058824
convert to tokens 1.441826367
 construct SA 0.325575006
height_to_group 0.17009132000000005
filter groups 0.10468057400000008
:len(list(groups)) 6197
calc score / per page grouping 0.011452530000000127
select good links 0.057980431000000276
:len(selected_links 2032
generate variant pages / make links 0.05053440300000034
output 0.0688222439999997
python3 scaffold_network.py  2.96s user 0.26s system 90% cpu 3.575 total
```


2倍ちょいのサイズの入力で2倍ちょい掛かって3秒
時間を食ってるのは前処理の部分で、コアの部分はまだ0.1秒くらい

:

```
:len(docs) 983
:all body length 698607
:average body length 710.6887080366225
convert to tokens 2.6240625730000002
 construct SA 0.7093633160000001
height_to_group 0.5530669490000006
filter groups 0.2120671629999995
:len(list(groups)) 13209
calc score / per page grouping 0.0323648960000007
select good links 0.14454357399999918
:len(selected_links 4751
generate variant pages / make links 0.1216121930000007
output 0.16785022500000046
python3 scaffold_network.py  6.59s user 0.53s system 93% cpu 7.605 total
```


さらに2倍にしたけど時間もおよそ2倍でおよそ線形
非線形部分の係数が小さくて目立たない
700文字1000文書で7秒なので現実的