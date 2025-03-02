
一連の話が複数人のウォールに別れてて混乱するのでいったんまとめた

- スピーカー同士で合唱をして重ねられるか→うまく重ならない、気持ち悪い [src](https://www.facebook.com/nishiohirokazu/posts/10223981308457088?comment_id=10223983418149829)
    - それを聞いてたオーディエンス「割とあってるように聞こえた」
    - 「オーディエンスからスピーカーへの昇格タイミングで1.5秒くらいの無音があった」
    - (正しくない推測) 僕の憶測だと、スピーカー同士はP2P接続をして、ローカルでミキシングしてると思う。オーディエンスはサーバサイドでミキシングされたものの配信をサーバから受けてると思う。
        - スピーカー同士で合唱しようとしたら気持ち悪かったが、オーディエンスにはまともに聴こえた、というのはそういうことかな、と思う。
        - この種のことを検証する方法が現場では思いつかなかったけど、時報を使うと良いと思う。
- パケットキャプチャの結果がきた
    - > 大久保 康平: clubhouse サーバーはおそらく東京にあり、スピーカー参加中もP2Pではなさそう。UDP ベースの独自プロトコルで、小さいパケットを大量にやりとりしているようです。以下、 Kengo Nakajima さんのログ [src](https://facebook.com/ohkubo.kohei/posts/10158086651341476)
:

```
送り先は以下の2箇所だけ
107.155.29.138 4005  これが9割以上
164.52.32.58 8913　　たまにこれが交じる
...
```

    - 通信先がほとんど1つであることでP2Pの可能性は明確に否定されたなぁ
        - ![image](https://gyazo.com/ed9d04fab21a5c921a6c379f4086531f/thumb/1000)
        - こういうことか
        - > Kengo Nakajima: 80バイトのパケットが毎秒50個みたいな勢い。zoomとか他とはだいぶ違う [src](https://www.facebook.com/ohkubo.kohei/posts/10158086651341476?comment_id=10158086740376476)
        - 赤線の部分がUDPベースの独自プロトコルということか
            - レイテンシーの小ささからサーバが日本にあるのは間違いなくて、金に任せて主要な国？都市？にサーバを置いてるのだろう。そのサーバ自体はUDPパケットを転送するだけのものかもしれないが。[src](https://www.facebook.com/kuchii.jun/posts/4194099850641216?comment_id=4194328553951679&reply_comment_id=4194340363950498)
                - あ、それと、スピーカー間がP2Pでないとしても「オーディエンスはサーバでミキシングされた後のストリームを少し遅れて受信してる」ってところは何も否定してないので、そこはそうなんじゃないかなー
    - > 高橋 達矢: IPで調べたらZenlayerというサービスで持ってるIPみたい。それの東京のアクセスポイントじゃないかな。[src](https://www.facebook.com/ohkubo.kohei/posts/10158086651341476?comment_id=10158086855531476)
        - [「エッジクラウド」で超高速データ処理を実現するZenlayer – TECHBLITZ](https://techblitz.com/zenlayer/?fbclid=IwAR2yvELVexps81wfsEWoN_u_HrGciqezxHYcUtFu7cFEIiA0eTaRjqXAQ1Q)
            - はー、なるほど。これでUDPパケットを高速に投げ返すエッジサーバを作ってるのか [src](https://www.facebook.com/nishiohirokazu/posts/10223986141217904)
            - 上記の図で小さい箱で書いたものがZenlayerということになる

綺麗な図解
- [https://www.facebook.com/kuchii.jun/posts/4194099850641216](https://www.facebook.com/kuchii.jun/posts/4194099850641216)

さらに詳しいパケットキャプチャ解説
- [https://gist.github.com/kengonakajima/31cb28404f4b96199fb9a84ea99c44f2](https://gist.github.com/kengonakajima/31cb28404f4b96199fb9a84ea99c44f2)

DNSパケットからの推測
- [https://zenn.dev/voluntas/scraps/9403b803320d6f](https://zenn.dev/voluntas/scraps/9403b803320d6f)
- ネットワーク構造的には同じ
- サーバで音声合成をしていないのでは、という意見
- > 自分が使いたいと思うのは E2EE が前提で ホワイトボードがある Clubhouse
    - あ、僕が欲しいのもそれだ笑
