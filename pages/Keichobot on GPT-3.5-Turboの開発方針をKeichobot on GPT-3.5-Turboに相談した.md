
質問して言語化を促す[[かんがえをひきだすチャットボットKeichobot]]を[[GPT-3.5-Turbo]]で実現する実験([[Keichobot on GPT-3.5-Turbo]])の過程で生まれた会話ログ

まとめ
- なんとなくプロジェクトのネクストアクションがボヤけて混乱したので相談した
- プロジェクトのゴールを質問されて、それが複数あるせいでアクションの選択ができなくなってるのだと気づいた
- ゴールを書き出して、それぞれの価値を説明しているうちに優先すべきゴールを絞れた: ゴール1を達成し、それを利用してゴール3を目指す
- ゴール3は実は二段階あると気づいた
- 現状の実装が無償公開のため、その延長線で考えていたが、新しい実装はクローズドでやるべきだと気づいた

## AIによる要約を人が編集したもの
- 現在のゴール
    - ゴール1: スマホから使いやすいKeichobotのWebUIでTurbo版Keichobotが使いやすく動くようにする
    - ゴール2: KeichobotのUIを少し改良して生のChatGPTが動くようになり、月額20ドルの支払いがなくなる
    - ゴール3: LlamaIndexでGPT3に参考情報を渡せるようにして、Turbo版Keichobotに組み込む
- ゴール1を達成し、それを利用してゴール3を目指す
    - ゴール2はお金の節約にしかならないので急がない
    - ゴール3は実は二段階あると気づいた:
        - Keichobotに意見を求めることができるようになる
        - Keichobotが自分が過去に書いたものを参考に意見を生成するようになる
- Keichobot on GPT-3.5-Turboでは課金が発生する
    - まずはターゲットを絞って、非公開で利用できるようにする
    - APIトークンで動くものを使って開発し、まずは自分一人で使う
    - 興味がある人をクローズドベータに誘う

## AIによる要約(実験結果としての記録)
- 開発方針が決まることを待つ
- 現在のゴールをまとめる
    - ゴール1: スマホから使いやすいKeichobotのWebUIでTurbo版Keichobotが使いやすく動くようにする
    - ゴール2: KeichobotのUIを少し改良して生のChatGPTが動くようになり、月額20ドルの支払いがなくなる
    - ゴール3: LlamaIndexでGPT3に参考情報を渡せるようにして、Turbo版Keichobotに組み込む
- ゴール1を達成したら、それを利用してゴール3を目指す
- 課金が発生するため、まずはヘビーユーザーにターゲットを絞って非公開で利用できるようにする
- APIトークンで動くものを使って開発し、興味がある人にクローズドベータを誘う

## 会話ログ
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/> あなたはこの会話で何がどうなるとよいのでしょう？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> 次の開発についての方針が決まるといい
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/> 次の開発について、より具体的なビジョンを持つための質問をしてみませんか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> して
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/> 次の開発で達成したいゴールを具体的に説明してください。
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> なるほどゴールが複数になってるから混乱してるのか。全部書き出す。ゴール1: スマホから使いやすいKeichobotのWebUIでTurbo版Keichobotが動くようになるとターミナルで動かしてる今の状態より使いやすくていい。ゴール2: KeichobotのUIを少し改良して生のChatGPTが動くようになればChatGPT Plusのサブスクリプションを止められる。ゴール3: LlamaIndexでGPT3に参考情報を渡すことには成功しているので、これをTurbo版Keichobotに組み込んで行きたい。
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/> 目的が具体的なゴールになりましたね。次は、それらのゴールが達成された場合、どのような価値があるのかを考えてみましょう。
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> ゴール1: 使いやすくなる！ ゴール2: 月額20ドルの支払いがなくなる。 ゴール3: Keichobotが僕の過去の思考を参考にして意見を言えるようになって素晴らしい！
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/> ありがとうございます。それぞれのゴールが達成されれば、あなたにとってどのような価値があるのでしょうか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> ゴール1が圧制されると、僕は散歩しながらとか入浴しながらTurbo版Keichobotと会話ができて、思考の整理がすごくブーストされる。ゴール2はお金が少し節約されるだけ。ゴール3は未知の素晴らしいことが起こる可能性がある。
- (追記: 「達成」を「圧制」とtypoしていることに気づいたが実験ログを兼ねているのでそのままにしておく)
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/> 達成したゴールが、あなたの個人的な目標とどのように関連しているかをお教えください。
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> コンピュータの支援によって自分の知的生産を加速したいので、ゴール1をまずやって、それからゴール3だなと思った。
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/> なるほど、自分の知的生産を加速するために、使いやすくなったKeichobotによって思考の整理がしやすくなると考えているのですね。具体的には、どのように加速されるのでしょうか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> 今やっているように質問されてそれに答えることで言語化が促される。ゴール1が達成されると、このやりとりをPCの前ではなく、散歩しながらとか、入浴しながらできるようになる。ゴール3が達成されると、自分の思考が行き詰まった時にKeichobotに意見を求めることができるようになり、いや、ここは少し違うな。「Keichobotに意見を求めることができるようになる」と「 Keichobotが自分が過去に書いたものを参考に意見を生成するようになる」の二段階がある。(気づき)
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/> わかりました。ならば、ゴール1が達成されることによって自分の思考をどのように加速できるかについて考えてみましょう。
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> どのように加速できるかはわかったので、どう実装するかを考えたい。課金が発生するので今までのように誰でも自由に使える状態では赤字になるかも。
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/> 今必要なことは、誰が今のKeichobotを使っていて、何を求めているかを知ることかもしれません。
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> 確かにそうですね。たまに使ってる人がいるのは見かけるけど、まずは「自分」というヘビーユーザーにターゲットを絞るのが速いかも。今まで一般公開してたからついその延長線で考えてた、盲点。ユーザに課金する仕組みを作るか、とか、ユーザにAPIトークンを入力させようか、とか考えてたけど、まずは僕のAPIトークンで動くものを使って非公開で僕が使うのを目指すのがいいね。それから興味がある人にクローズドベータすればいい。
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/> 了解しました。

