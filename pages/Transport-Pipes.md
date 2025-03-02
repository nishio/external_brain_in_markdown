
マイクラにパイプを導入するプラグイン
- ホッパーやドロッパーで無理矢理パイプ的なことを実現しないでよくなる

普通のパイプ
- ガラス4つで作業台で作る

金のパイプ(Golden Pipe)
- アイテムの振り分け機能がある
- 色は繋ぐパイプの色ではなく継ぎ目に表示されているもの
- 指定したもの「以外」を通す設定もできる
- 金ブロックが必要
- 最初にすごく便利だ！と思ったが他のパイプを理解するにつれてだんだん価値が下がっていった

抽出パイプ(Extraction Pipe, 吸い出しパイプ)
- チェストなどの中にあるものをパイプに移す機能を持ったパイプ
- 実はこれにも何を吸い出すかのフィルタがある
    - つまり金のパイプの代わりにチェストと抽出パイプでも同様のことができる、金ブロックはコンパクトなだけ
- レッドストーンで制御されるように設定できる
- 一度に輸送するスタックサイズを16にすることができる
    - 中身の詰まったチェストを他のところに動かしたい時とかに便利
- Direct設定については後述
    - 物理的には不自然な挙動をするが超便利

色のついたパイプ
- 違う色のものは接続しないのでコンパクトな配管ができる
    - ただし普通の白いパイプはどれともつながる
    - なおパイプの断面図をレンチで叩いて同じ色でも接続しないように設定できる

パイプでかまどに物を入れることができる
- 焼くものは上と側面、燃料は側面からのみ、成果物の吸い出しは下から

クラフトパイプ
- クラフトできる
- 例えば石炭を自動で石炭ブロックにしてからチェストに入れられる

オフィシャル解説はこちら
- 5.0.0 for Minecraft 1.13 [https://www.spigotmc.org/resources/transport-pipes.20873/](https://www.spigotmc.org/resources/transport-pipes.20873/)
    - ただしこの5.0.0は1.17に非対応
- こちらの5.3.0が良い  [https://github.com/BlackBeltPanda/Transport-Pipes/releases](https://github.com/BlackBeltPanda/Transport-Pipes/releases)
- 5.4.0で1.18に対応した

Direct設定とはなんなのか
- Tweet
    - > [nishio](https://twitter.com/nishio/status/1438919182934966279): ええー、パイプの中を流れるアイテムがパイプの分岐に来た時に別れるかどうか、チェストから吸い出した時の吸い出しパイプの属性で決まるの〜？マジか〜
    - > [nishio](https://twitter.com/nishio/status/1438925551108984832): いやー、これオプションによっては「来た方向以外のパイプのうち0番目のものに全部送る」になって、その0番目とは方位を表すenumの順番で決まるからパイプの向きによって挙動変わるんじゃないの？？
        - これがDirect設定
    - > [nishio](https://twitter.com/nishio/status/1438927890440089604): はい正解、左の配置ではアイテムが直進して松明の側のチェストに入り、右の配置ではアイテムは右折し松明の付いたチェストに入る。東西方向のパイプが南北方向のパイプより優先されるからである。
        - ![image](https://gyazo.com/5ffeff86977c1057c4b9fdd5d2cce0a5/thumb/1000)
    - > [nishio](https://twitter.com/nishio/status/1438929863927160833): これを踏まえると自動仕分けチェストはなんとこれだけで実現できる。画面前後方向が東西なので優先され、左のチェストから順に「そのチェストに入るなら入れる、無理なら右のパイプへ」という振る舞いをする。
        - ![image](https://gyazo.com/e1a30e49903d5ac3585f5de9a6dd4f98/thumb/1000)
    - > なお上下が一番優先度低いので縦に積むなら四方の向きは自由になる。

Javaがわかる人向け解説
- アイテムがDIRECTモードなら可能な移動方向選択肢の最初なものに全部送る
    - [ItemDistributorService.java#L119](https://github.com/BlackBeltPanda/Transport-Pipes/blob/33dfb9aaf42438405328511b5e5235b416c33ef0/src/main/java/de/robotricker/transportpipes/duct/pipe/filter/ItemDistributorService.java#L119)
java

```
if (pipeItem.getExtractMode() == ExtractMode.DIRECT) {
    splitMap.put(weightsDirectionList.get(0), item.getAmount());
}
else {
```

- 可能な移動方向とはパイプの繋がってる方向から、そのアイテムがやってきた方向の逆方向を除いたものである
    - [Pipe.java#L329](https://github.com/BlackBeltPanda/Transport-Pipes/blob/33dfb9aaf42438405328511b5e5235b416c33ef0/src/main/java/de/robotricker/transportpipes/duct/pipe/Pipe.java#L329)
java

```
protected Map<TPDirection, Integer> calculateItemDistribution(PipeItem pipeItem, TPDirection movingDir, List<TPDirection> dirs, TransportPipes transportPipes) {
	Map<TPDirection, Integer> absWeights = new HashMap<>();
	dirs.stream().filter(dir -> !dir.equals(movingDir.getOpposite())).forEach(dir -> absWeights.put(dir, 1));
	return itemDistributor.splitPipeItem(pipeItem, absWeights, this);
}
```

- 「方向」とは東西南北上したの順で定義されたenumである
    - [TPDirection.java](https://github.com/BlackBeltPanda/Transport-Pipes/blob/33dfb9aaf42438405328511b5e5235b416c33ef0/src/main/java/de/robotricker/transportpipes/location/TPDirection.java)
:

```
public enum TPDirection {
    EAST(1, 0, 0, BlockFace.EAST, LangConf.Key.DIRECTIONS_EAST.get()),
    WEST(-1, 0, 0, BlockFace.WEST, LangConf.Key.DIRECTIONS_WEST.get()),
    SOUTH(0, 0, 1, BlockFace.SOUTH, LangConf.Key.DIRECTIONS_SOUTH.get()),
    NORTH(0, 0, -1, BlockFace.NORTH, LangConf.Key.DIRECTIONS_NORTH.get()),
    UP(0, 1, 0, BlockFace.UP, LangConf.Key.DIRECTIONS_UP.get()),
    DOWN(0, -1, 0, BlockFace.DOWN, LangConf.Key.DIRECTIONS_DOWN.get());
```

