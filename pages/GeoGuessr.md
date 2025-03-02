
[/geoguessr-nishio](https://scrapbox.io/geoguessr-nishio)

2023-01-22 from [/villagepump/GeoGuessr](https://scrapbox.io/villagepump/GeoGuessr)
- [[GeoGuessr]]の4対4チーム戦にいきなり参戦してきた<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
    - もっと予習が必要だ！

2019-05-12
- ランダムな位置のグーグルアースが表示される
- それが地球上のどこであるのかを当てる
- [https://geoguessr.com/](https://geoguessr.com/)

- iOS版を購入した
    - 地球全体でのランダムが無料
    - Famous Place、Major Citiesなどは360円払って買うか、プレイすることによってたまるポイントで買う
- 個人的にはFamous Placeをサクッと課金して買うのがおすすめ
    - 「あっ、これはルーブル美術館だな！」みたいな感じのプレイ感になる

ゲーム構造に関する考察
- 画像+αを入力として、位置を出力とするクイズゲーム
- よくあるクイズ番組と違って、出力が「単語」ではなく「位置」なのが面白いポイント
    - 正解の位置との距離でスコアが決まる
    - ある画像を見てA:「あー、南米にある、なんだっけー」という状態とB:「これはマチュピチュ！」という状態は「単語のクイズ」では勝敗が分かれる(B>>A)が「位置のクイズ」ではC:「マチュピチュはインドだったかな？」なんて状態だとAの方が点数が高くなる(A>>C)
    - ピサの斜塔がイタリアにあることがわかっても、ピサがどこにあるかわからないと点が伸びない。
    - というわけで繰り返しプレイしている間に「言語的でない知識」が育っていくのが実感できて面白い
        - 「ピサはイタリアのあの辺にある」
        - Google Mapの仕様上、マイナーな場所ほどズームインしないと表示されない
            - ![image](https://gyazo.com/20687fc9d3f7ba500da5e35ac90a10e9/thumb/1000)
        - だいたいどの辺にあるかがわかれば、その辺りをズームインすると見つかる
            - ![image](https://gyazo.com/a862985cfd99cdecbb750ec8a3815794/thumb/1000)
        - モンサンミッシェルはフランスにあるのだけど、さてどこでしょう。
    - 逆に「位置の知識が言語化されて格納される」というケースもあって面白い
        - 「マチュピチュはどこにある？」
        - 「南米にある」
        - 「チリではなくペルーにある」
        - 「ペルーのクスコにある」
        - ![image](https://gyazo.com/4cf787c8dc9e6bdc64c86a678c52d419/thumb/1000)
        - 「クスコの北西のAguasなんとかにある」
        - ![image](https://gyazo.com/880db7c1be8a3b6274e76945f69df911/thumb/1000)
        - 「あった！」
        - ![image](https://gyazo.com/8372cea96260473c843266bfa9db9313/thumb/1000)



- 四角い修道院の場所がなかなか覚えられない
- 半円形の城の場所が覚えられない

