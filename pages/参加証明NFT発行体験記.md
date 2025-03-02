---
title: "参加証明NFT発行体験記"
---

> [@nishio](https://twitter.com/nishio/status/1664149996361633797?s=20): [[貢献の可視化]]や[[参加の可視化]]の実験で[[未踏ジュニア]]コミュニティに参加している人に「[[参加証明NFT]]」を発行してみる実験をした。
> ![image](https://gyazo.com/f8e4737e338bd2cafe62210577b66f11/thumb/1000)
> [@nishio](https://twitter.com/nishio/status/1664153160188071936?s=46&t=gkSZtjGEtUZPO0JCzBxCBw): 実験したのはもう少し前なんだけど体験談記事を書くのが追いついてないのでとりあえず実験をやったということだけ書いた、詳しい話は後ほど。

[[PluralityTokyo]]で「イベントに参加したことを証明するNFTが受け取れる」とアナウンスされて面白そうなので取得した。
- [[参加証明NFT取得体験記]]

[[Social Hack Day #50]]で発行する側にも興味があるという話をしたらテストネットで発行する側の体験ができた。
- 費用感
    - 相場が変動するので確約はできないが、大体1件5〜15円くらいとのこと
    - ステッカーを作って配ることと比較したら安い
- ステッカーと違って「持っていたら何々ができる」や「たくさん集めるとレベルアップする」などの発展性があって面白そう
- リアルに発行したい気持ちが高まった

未踏ジュニアのイベントで参加証明NFTを出すことをリーダーの鵜飼さんにOKもらった
- ダメだったら「西尾と会った証明」という形にして個人で配るつもりだった
    - [[Joi POM]]みたいに
    - ![image](https://gyazo.com/f27ba704d6a1b0ee79a29662848c853b/thumb/1000)

[MugiSus](https://twitter.com/mugisus)さんがデザインして未踏ジュニアのScrapboxでFaviconとして使われている画像を使って良いか聞いてOKをもらう

# MATICの用意
画像と説明文は用意して、さあ発行しようとして、先にMATICを用意する必要があったことに気づく
- ![image](https://scrapbox.io/files/647b9279297db6001cb025f4.png)
- 実は1番のハードルはMATICの用意だった

## Day 1
CoincheckでEthereumを持っていたので、1万円分くらいMATICに変えたらいいやと思った
- →CoincheckでのMATICの取り扱いがない

MATICを入手する方法を調べたが、Google検索結果のどれが信用できる情報なのか判断できなかった。
- 報告
    - 画像と説明文は用意できた
    - 発行しようとしてMATICを用意する必要があったことに気づく
    - MATICの買い方がわからないので調べる
        - 1: ネットで検索した記事
            - 1-1: MATICを買える取引所(ビットポイント)の口座を作れという記事
            - 1-2: XRPを買ってBybitで交換しろという記事
            - 1-3: MetaMaskで買える、ただしクレジットカード会社が拒否するかも、という記事
    - 1-3を試す→購入ボタンのリンク先が表示できない(日本国内からアクセスできないとか？)
    - 次は1-2を試そうと思うがその前にここまでをまとめてシェアした方がいいなと思った

[https://discord.com/channels/979969380802777169/980097978792562728/1112321547949047868](https://discord.com/channels/979969380802777169/980097978792562728/1112321547949047868)
- 方法2
    - 日本円にペグされた[[JPYC]]を使う経路
        - [https://app.jpyc.jp/](https://app.jpyc.jp/)
        - 支払い方法は銀行振込
        - ウォレットアドレスに直接トークンをおくってくれる
        - [[Uniswap]]などの暗号通貨交換所でMaticと交換する
- 方法3
    - NativeのMATICを交換所で購入できる
        - SBIの含め3箇所で販売されている

## Day2
- SBI VCトレードの口座開設申請をした

## Day3
口座ができた
- 入金する
- とりあえず1万円

[サポートコンシェルジュ｜SBI VCトレード｜暗号資産（仮想通貨）・口座開設](https://www.sbivc.co.jp/faqs/content/im05m6ohz4kr)
![image](https://scrapbox.io/files/647b92fee804c6001c7882ee.png)
- みずほはサポート対象外なのか？
- 住信SBIにした

即時決済サービスを使う
- ![image](https://scrapbox.io/files/647b93275e524b001b90b499.png)
- すごい便利な時代だなぁ
- (ずっと使ってるみずほをいい加減にやめてこういう新しいことをできてるところをメインにしようと改めて思った)

![image](https://scrapbox.io/files/647b93de68fd14001ca4cef3.png)
- 75MATIC買うことにした
- ![image](https://scrapbox.io/files/647b93ebd50be1001c90bab5.png)
- 買えた

SBI VCの口座を作ってMATICを買うところまではできた
- が、それをMintRallyで使うために自分のウォレットに送る方法がわからなくて詰まっている。
- 「SBI Web3ウォレット」なるものをMetaMaskと繋ぐことはできて、そこにNFTなどは表示されているが…
- あっ、わかった、デフォルトでは暗号資産のやり取りのメニューが表示されてない素人向けUIなんだ。
- 「トレーダーモード」というものに切り替えたら「暗号資産出庫」のメニューが出てきた(自己解決)

暗号資産出庫しようとする
- 出庫するためには先に出庫先の登録が必要
- 出庫先登録しようとする
    - フォームを埋め終わってから第二暗証を要求されることに気づく
    - 第二暗証とは？
    - 二要素認証の設定をする必要がある

出庫先登録できた
- とりあえず1MATICだけ出庫してみる
- 「出庫予約メール」なるものが届いた
- そのメールのリンクをクリックすると「出庫予約を受け付けました」になる
    - 完了したらメール連絡がくるらしい、待つ
- 関連
    - > 当社は2022年9月28日より、トラベルルールへの対応に伴い、新たにお客さまが暗号資産の出庫（外部送付）を行う際に、「移転の目的」に関する情報の取得・保存を開始いたします。
    - > 詳細は以下をご確認ください。
    - >  [https://www.sbivc.co.jp/newsview/ey85rsne242r](https://www.sbivc.co.jp/newsview/ey85rsne242r)

なかなか来ない
- 【SBI VC Trade】出庫予約を受け付けました 11:47 AM
- 【SBI VC Trade】出庫完了のお知らせ 3:30 PM
- 3時間も掛かるんだ
- 出庫できてた
    - ![image](https://scrapbox.io/files/647b94c0e79e21001c0a035a.png)

イベントグループ作成
- ![image](https://scrapbox.io/files/647b9513d75822001c3072ba.png)
- 3セントくらい支払う

イベント作成をしようとするとエラー
- "insufficient funds for gas * price + value: address 0xd50... have 966546521347084996 want 11345890700340000000"
    - なるほど 1MATICでは足りない
- ガス代肩代わり(僕がガス代を払って、受け取る人は無料)の設定にしているのだが、特に根拠なく「受け取りが発生するたびに僕のアドレスから引き落とされる」と勘違いしていた
    - そうではなく、初回に決めた最大人数分を先払いだった
        - この時は100人にしていた
        - 1ドルくらいしか入れてないのに10ドルくらい支払おうとしてるからそれは無理だ

発行枚数を10枚にする
- それでも足りない旨のエラー
- 深夜だったのでガス代が高かった
- ![image](https://scrapbox.io/files/647b9801dea9ec001cecd2a7.png)
- [https://polygonscan.com/gastracker](https://polygonscan.com/gastracker)
- 残りの74MATICの出庫をして寝る
    - まあでも最初から75MATICで試してたらガス代が高いことにも先払いなことにも気づかずに100枚発行してたと思うので学びは最大化された

## Day 4
11:00
- ![image](https://scrapbox.io/files/647b98e0c58ab4001c5c7f86.png)
    - なるほど、昨日の半額以下だ
- 24時間のグラフ
    - ![image](https://scrapbox.io/files/647b98fd297db6001cb0309a.png)
- 1週間のグラフ
    - ![image](https://scrapbox.io/files/647b9901313b1b001cc658c7.png)
    - [https://livdir.com/polygongaspricechart/](https://livdir.com/polygongaspricechart/)
- なるほどなー、夜は高い

10枚発行
- ![image](https://scrapbox.io/files/647b998dc75d27001c47332b.png)
- 76セント支払い、ガス代が14セント掛かって、合計90セント
    - 普通のガス代でギリギリ1MATICだから、深夜の高いガス代では成立しないのも当然だったな

イベントページが作成できた！
- ![image](https://scrapbox.io/files/647b9a7fb3b062001babaf5e.png)

イベントページからNFTの取得ができた！
- ![image](https://scrapbox.io/files/647b9a8eb978c0001b12056d.png)

[[OpenSea]]でも僕の所有しているNFTとして表示されている
- ![image](https://gyazo.com/f8e4737e338bd2cafe62210577b66f11/thumb/1000)
- OpenSeaでは最初は「その他」「非表示」の中にある
- ![image](https://scrapbox.io/files/647b9bb358113f001bb50f3c.png)
- 「再表示」をすると他の人にも見えるようになる


サービスの解説
- [MintRally](https://www.mintrally.xyz/ja)
- > [[MintRally]]はシビックテックプロジェクト[[Hackdays]]のメンバーで開発しているオープンソースプロジェクトです。
- >  機能拡充やユーザビリティの向上、アクセシビリティへの対応などに取り組みながら、よりよいオープンソースプロジェクトにしていくための仲間を探しています。
- Discordのリンクがある [https://discord.com/invite/4hJefCEYKS](https://discord.com/invite/4hJefCEYKS)
    - 僕は[[Social Hack Day #50]]に参加したときに入った
    - MATICを入手する方法とか、一人だったら挫折してたかも
- Social Hack Day自体が参加証明NFTを発行している
    - ![image](https://gyazo.com/d68b0457b8780640055fe9f667805995/thumb/1000)
    - [[ドッグフーディング]]
- 意外なことに、現状このサービス自体はデータを持っていない(=全部ブロックチェーンに置いてる)
    - それでこのようなサービスが実現できるというところが面白い、パラダイムの変化を感じる