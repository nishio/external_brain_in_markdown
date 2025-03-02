---
title: "xz-utilsバックドア事件"
---

[Everything I know about the XZ backdoor](https://boehs.org/node/everything-i-know-about-the-xz-backdoor)
[xz-utils backdoor situation](https://gist.github.com/thesamesam/223949d5a074ebc3dce9ee78baad9e27)

<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>xz-utilsバックドア事件の概要は以下の通りです。
- 2024年3月29日、広く使われている圧縮ソフトウェアxz-utilsにバックドアが発見された。
- バックドアは、xz-utilsのメンテナーであったJia Tanによって仕込まれたと見られている。Jia Tanは2年ほど前からxz-utilsの開発に関わるようになり、次第に信頼を得ていた。
- バックドアは非常に巧妙に作られており、特定の条件下でのみ発動するようになっていた。主にsystemdとopensshを使っているLinuxシステムが標的だった。
- バックドアが発動すると、sshの認証を迂回してシステムに侵入できるようになる。ただし、現時点ではこれ以外の影響は不明。
- Jia Tanは、別のアカウントを使ってバックドアを含むパッチを強く推すなどの不審な行動も見せていた。
- メインのメンテナーであるLasse Collinは休暇中で、Jia Tanの活動を止められなかった。オープンソース開発者の過酷な状況が背景にあるとの指摘もある。
- Jia TanのGitHubアカウントは凍結され、バックドアは除去されたが、その他の影響は調査中。xz-utilsを含む多数のシステムが調査・更新を迫られている。
以上のように、長期的な信頼関係を築いた開発者による内部からの攻撃であり、オープンソース・ソフトウェアの脆弱性が改めて浮き彫りになった事件と言えます。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
- "systemdとopensshを使っているLinuxシステム"はとてもメジャーなデジタル社会のインフラであり、それに「侵入可能」になる「バックドア」とは、エンジニアでない人向けに例えるならどの扉でも開けられるマスターキーのようなもの。
- 幸い今回の細工は広く導入される前に発覚したが「見つかりやすいものから見つかる」という考えから「うまく潜伏してまだ見つかっていない細工があるのでは」と懸念する声がある
- また、侵入するシステムと一見無関係で注目されにくい圧縮ソフトウェアを糸口とし、長期的な信頼獲得行動をした上でメインメンテナーの個人的事情を利用して犯行に及んだ行動が、一個人の自発的動機ではなくたとえば国家や反社会的組織などのスポンサーの存在を示唆している、と考える人もいる。これに関しては[[陰謀論]]であるのか正しい推測であるのか判断できる明確な証拠がない


> [dmikurube](https://twitter.com/dmikurube/status/1773975696526000129) すげえな。三年かけて信頼関係を築きバックドアを仕込む。千年かけて魔族を騙すような所業だけど、これくらいなら実際インセンティブあるよなあ…  [Everything I know about the XZ backdoor](https://boehs.org/node/everything-i-know-about-the-xz-backdoor)
> [dmikurube](https://twitter.com/dmikurube/status/1773979679810257118) こういうののメンテナンスが個人の肩に乗ってる現状も、これを検知したのがほぼ個人の職人芸に依るものだったというあたりも、もうなんというかねえ
> [dmikurube](https://twitter.com/dmikurube/status/1773981126643814479) しかし一つこれがあったということは、他にもあると見るべきなんだろうなあ。うへえ
> [dmikurube](https://twitter.com/dmikurube/status/1773983031025664412) オープンソース文化圏は「コントリビューション待ってまーす☆」みたいなノリも多いけれども、こういう例を見ると難しいよねえ。「なんで俺の PR が全然マージされねーんだ!」みたいな文句を言っている人もたまに見かけるけど、メンテナーとしてはそんな軽々に受け入れらんないっすよそりゃ
> [dmikurube](https://twitter.com/dmikurube/status/1773983943001567495) (そういう文句を言っている人のことはかなーり苦々しく思っております。自分がメンテナーやってるものでなくても)
> [dmikurube](https://twitter.com/dmikurube/status/1773986943933862360) 実際 Embulk なんざ、ちょっと細工を忍び込ませられれば、各社のデータを横流しするくらいのことができちゃうだろうからね。いちおう慎重に見てはいますよ。プラグインは管轄外のものが多いけど
> [dmikurube](https://twitter.com/dmikurube/status/1773987824494370841) GitHib Actions なんかも、うかつにサードパーティーの Action を使ったりなんかはしないようにしている。なんか仕込むには格好のターゲットだからね。あと典型的なのは Gradle プラグインとかな
> [dmikurube](https://twitter.com/dmikurube/status/1774035020199710776) "In April 2022, Jia Tan submits a patch via a mailing list. The patch is irrelevant, but the events that follow are. A new persona – Jigar Kumar enters, and begins pressuring for this patch to be merged." わぉ。「これマージしろ」ってプレッシャーかける輩は同類判定でいいんでないか
>  「2022年4月、Jia Tanはメーリングリストを通じてパッチを提出しました。パッチは無関係ですが、それに続くイベントは無関係です。新しいペルソナ – ジガー・クマールが入ってきて、このパッチをマージするよう圧力をかけ始めます。 わぉ。「これマージしろ」ってプレッシャーかける輩は同類判定でいいんでないか
> [dmikurube](https://twitter.com/dmikurube/status/1774035165444296802) "Soon after, Jigar Kumar begins pressuring Lasse Collin to add another maintainer to XZ. In the fallout, we learn a little bit about mental health in open source." うーむ…
>  "その後すぐに、Jigar Kumar は Lasse Collin に XZ に別のメンテナを追加するよう圧力をかけ始めました。その結果、オープンソースでメンタルヘルスについて少し学ぶことができます」 うーむ...

> [izutorishima](https://twitter.com/izutorishima/status/1773959339629498628) すごい、3年がかりで xz-utils に貢献して信頼を勝ち取った上でバックドアを仕込んだらしい　エグすぎるだろ……
>  見つけられたのは本当に偶然としか言いようがないし、もし Ubuntu とかまで回ってたら sshd 出してる全ての公開サーバーにパスワードなしでログインできることになって怖すぎる

> [piro_or](https://twitter.com/piro_or/status/1774059039812645020) [[colors.js]]の騒動は開発者自身が物事をぶちこわしたというもので、べつにオープンソースだからというものではない、[[WinGroove事件]]と同様のソフトウェア一般の話だと思うけど、コントリビュートで信頼を積み重ねてコミット権限まで得た上で攻撃者となるのは、オープンソースならではの話だなと思う。
> [piro_or](https://twitter.com/piro_or/status/1774061170259067265) WinGroove事件、今だと不正電磁記録うんたらで捜査の対象になりえただろうか。

> [nishio](https://twitter.com/nishio/status/1774001859545674130) 「見つかった不正は隠蔽工作が下手くそな不正」の法則で考えると、xzに遠隔ログインバックドアが仕掛けられていたのが見つかって今のうちに対処出来てよかったね……というよりは、知られてない何かに同じようなバックドアが仕掛けられていて広まっている可能性があるよな。

> [Cryolite](https://twitter.com/Cryolite/status/1774300154566455736/photo/1)
>  ![image](https://pbs.twimg.com/media/GJ-URGkaIAALUI9?format=png&name=small#.png)

[[オープンソースのジレンマ：イノベーション、セキュリティ、そして持続可能性のバランス]]

[[サイバー犯罪]]
[[サイバー戦]]
