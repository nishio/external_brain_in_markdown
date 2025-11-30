---
title: "SimEarth"
---

[https://www.myabandonware.com/game/simearth-the-living-planet-10c/play-10c](https://www.myabandonware.com/game/simearth-the-living-planet-10c/play-10c)
- モノクロだった気がするし、ウィンドウがもっと広かったと思うけど、確かにこんな感じだった

---

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>子供の時に親戚の家のMacでSimEarthをプレイした気がする。モノクロだった。マニュアルにガイア理論と白黒のデイジーによる気温調整が書かれていた気がする。可能なら再度プレイしてみたい。調べて

<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>
たぶんそれ、SimEarth: The Living Planet（シムアース）の初期Mac版ですね。
[https://www.mobygames.com/game/1835/simearth-the-living-planet/screenshots/macintosh/522019/?utm_source=chatgpt.com](https://tse4.mm.bing.net/th/id/OIP.dFXh2AV_s4A__GoYLkwa9AHaFj?pid=Api)

当時の記憶は合ってる？

1. [[ガイア理論]]と[[デイジーワールド]]
- SimEarth は ジェームズ・ラヴロックのガイア仮説をベースにした惑星シミュレーションで、ラヴロック本人がアドバイザーとして参加＆マニュアルの序文も書いています。([ウィキペディア](https://en.wikipedia.org/wiki/SimEarth?utm_source=chatgpt.com))
- マニュアルの中に **「TESTING THE GAIA HYPOTHESIS — DAISYWORLD」**という節があり、
        - 黒いデイジーは光を吸収して惑星を暖める
        - 白いデイジーは光を反射して惑星を冷やす
    - という説明がちゃんと書かれています。([インターネットアーカイブ](https://archive.org/stream/Mac_SimEarth_manual/SimEarth%20manual_djvu.txt))
- さらに後半の章で、
        - 「暗い・明るい・中間色のデイジー」が出てくる
        - アルベド（反射率）を通じて惑星平均気温が自己調整される
    - という Daisyworld の解説もあります。([インターネットアーカイブ](https://archive.org/stream/Mac_SimEarth_manual/SimEarth%20manual_djvu.txt))
- → 「白黒のデイジーで気温調整する」という記憶はかなり正確です。

2. モノクロのMac版について
- マニュアルには「マニュアルの画面写真は Macintosh モノクロ版と IBM Hercules/MCGA モノクロ版のものを使っている」と明記されていて、初代Mac向けの白黒バージョンがあったことがわかります。([インターネットアーカイブ](https://archive.org/stream/Mac_SimEarth_manual/SimEarth%20manual_djvu.txt?utm_source=chatgpt.com))

今プレイするにはどうする？
残念ながら、公式のダウンロード販売（GOGやSteamなど）では今のところ出ていません。GOG には「出してほしい」というウィッシュリストだけがあります。([GOG](https://www.gog.com/wishlist/games/simearth_the_living_planet?utm_source=chatgpt.com))
なので、現実的な選択肢は「エミュレータ＋古い版」です。

A. いちばん手軽：ブラウザでDOS版を触ってみる
雰囲気だけすぐ思い出したいなら：
1. 「SimEarth My Abandonware」などで検索すると、
ブラウザ上で DOS 版をそのまま動かせるページがあります（内部的には DOSBox）。([My Abandonware](https://www.myabandonware.com/game/simearth-the-living-planet-10c?utm_source=chatgpt.com))
2. ページを開くと、自動でゲームが起動するので、キーボードとマウスで操作。
※ 著作権的にはグレー寄りなので、「保存目的のアーカイブを利用している」という意識で使う感じです。

B. ちゃんと自分のMac上で遊ぶ：DOSBox＋DOS版
macOS（10.15）なら、DOSBox で DOS 版を動かすのが現実的です。([Abandonware DOS](https://www.abandonwaredos.com/abandonware-game.php?abandonware=SimEarth&gid=631&utm_source=chatgpt.com))
ざっくり手順：
1. DOSBox をインストール
    - 「dosbox mac ダウンロード」あたりで公式サイトから入手。
2. SimEarth の DOS 版のディスクイメージかフォルダを用意
    - 既にフロッピーやCDなどの現物を持っていれば、それをイメージ化して使うのがクリーンなやり方。
    - 所有していない場合でも、いわゆる abandonware サイトに DOS 版がアーカイブされていますが、ここは自己責任ゾーンです。([My Abandonware](https://www.myabandonware.com/game/simearth-the-living-planet-10c?utm_source=chatgpt.com))
3. DOSBox でフォルダをマウントして起動
    - 例：`mount c ~/games/simearth` → `c:` → `simearth.exe` のような感じで起動。
UI や内容は当時のMac版とほぼ同じで、Daisyworldシナリオも入っています。([ウィキペディア](https://en.wikipedia.org/wiki/SimEarth?utm_source=chatgpt.com))

C. 「Macらしさ」にこだわるなら：クラシックMacエミュレータ＋Mac版
「どうしてもMacの感じでやりたい！」場合：
1. Basilisk II / SheepShaver などのクラシックMacエミュレータを用意。
2. System 7〜9 のインストールイメージと、SimEarth の Mac 版を用意。
3. 起動して、当時の白黒〜16色時代のMac環境ごと再現。
Mac版は「SimClassics 2」という SimCity・SimEarth・SimFarm のセットがディスクイメージとしてアーカイブされていたりします。([macintoshrepository.org](https://www.macintoshrepository.org/52950-simclassics-2?utm_source=chatgpt.com))
こちらもセットアップは少しマニアックですが、「親戚の家のMac」感に一番近づけます。

ざっくりいうと：
- 記憶している「ガイア理論＋白黒デイジー」のゲームは、ほぼ間違いなく SimEarth。
- その説明は確かにマニュアルに詳しく載っている。
- 今すぐ軽く触るだけなら「ブラウザ版のDOSエミュ」、
- ちゃんと腰を据えてやるなら「DOSBox」「クラシックMacエミュ」のどれか、という感じです。
どのルートで遊びたいか決まったら、その方法に絞ってもう少し具体的な手順を書きます。
