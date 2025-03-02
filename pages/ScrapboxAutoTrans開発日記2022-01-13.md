
prev [[ScrapboxAutoTrans開発日記2022-01-12]]

一部他の人にも有益な機能があると思うけど「自分のニーズを満たす」「他人のニーズを満たす」を同時にやろうとすると混乱するのでまずは自分のユースケースに邁進しようと思う

つまり、まずルーティングのところを変えて自分のプロジェクトだけホワイトリストで通すようにし、他のプロジェクトとの衝突を気にせずに自由に使えるようになったURLパターンを使いたいものに使っていく

---
`relatedPages.links2hop[].linksLc`
の内容は
`relatedPages.links1hop[].titleLc`
に含まれないことがある。
具体的にはX→Y→ZのリンクでYが存在しないページの場合。

こうした
- > ![image](https://gyazo.com/403dba866dcebf842d87fcba6fb93720/thumb/1000)

---
ルーティングテーブルを書き換えたいのに設定ファイルが全然見つからないぞ？と思ったが、ファイルの配置で表現するスタイルなんだそうだ

defaultのexportをした関数がビューで、他にgetStaticPropsとかの特定の名前でエクスポートされてるものがある
---
静的なページの一部だけ動的にするとか、管理者だけメニューを出すとかってどうやるのかな

---
カスタマイズしたトップページ
- > ![image](https://gyazo.com/6438e371e7b01cb8423bfa790251ff14/thumb/1000)

あー、ページタイトルが出ちゃうか、まあそうかー
特定のファイル名のコードブロックを隠す機能と、タイトルなしでレンダリングする機能があれば良い

---
できた
> ![image](https://gyazo.com/8189ce957cf5d80098a337d384f40d19/thumb/1000)
元データは[[INDEX_FOR_VERCEL]]

---
オーナーが違う複数の個人プロジェクトの融合とか、個人プロジェクトとオープンプロジェクト(誰でも入れるプロジェクト)の融合とかも色々面白いことが起きそうな予感があるが、ブレずにまずは自分の目的をきちんと達成しよう

自分の目的は「オーナーが自分である日本語の個人プロジェクトと、オーナーが自分である英語の個人プロジェクトの融合」
- [/nishio](https://scrapbox.io/nishio)
- [/intellitech-en](https://scrapbox.io/intellitech-en)

`/ja/{title}`と`/en/{title}`で出しわけしようかと思ってた
- 読者が日本語話者かどうかで出しわけするの、本当に必要？
- そもそも日本語話者かどうかどうやって判別するの

![image](https://gyazo.com/d6bf9335203efd3880b84ed7c1a01691/thumb/1000)

- これでいい気がする

---
被リンクが表示されてないな
![image](https://gyazo.com/8773a16c6beae7df133ac0a39e2e4527/thumb/1000)
![image](https://gyazo.com/de08b80e7999936b7ce3d3bdd84929ab/thumb/1000)

links1hopから作るべきか
fixed: [https://github.com/nishio/scrapbox-reader/commit/efbcdf50e15e41a4e6fbd1303863a401f74d6a25](https://github.com/nishio/scrapbox-reader/commit/efbcdf50e15e41a4e6fbd1303863a401f74d6a25)

---
こういうシチュエーションで2hopリンクは繋がらない(灰色は存在しないページ)
![image](https://gyazo.com/5ce3067b14ff6bb0dfd3edf56c660807/thumb/1000)

---
ENにあるページから、そのプロジェクトにないページへのリンクをクリックして、JAのページが表示されるようになった
- つまりこういうこと
    - ![image](https://gyazo.com/9241812e18871f937d2632db37e74b7b/thumb/1000)
- ただし、遷移後にリロードが必要
    - なんかキャッシュ周りで間違ってるんだろうな
- [https://scrapbox-reader-six.vercel.app/en/Jiro_Kawakita](https://scrapbox-reader-six.vercel.app/en/Jiro_Kawakita)
    - ![image](https://gyazo.com/d5965a3448a5fbac3bb11779f65f8f48/thumb/1000)
- [https://scrapbox-reader-six.vercel.app/en/川喜田_二郎](https://scrapbox-reader-six.vercel.app/en/川喜田_二郎)
    - ![image](https://gyazo.com/3aabffe56e4d3c1337aff6431b14eb3d/thumb/1000)
        - ![image](https://gyazo.com/d9b8628e2daf55c2dbbf28055cb7fdc1/thumb/1000)
            - ![image](https://gyazo.com/511e592b4ce873bfa08034420d952f7c/thumb/1000)

---
> こういうシチュエーションで2hopリンクは繋がらない(灰色は存在しないページ)
>  ![image](https://gyazo.com/5ce3067b14ff6bb0dfd3edf56c660807/thumb/1000)
- というときに、繋がって欲しければJAに中身のないページを作ればいいのでは？と思った

before
- ![image](https://gyazo.com/6ea34b61ecec16f65e33eae43fe57ab0/thumb/1000)
do
- ![image](https://gyazo.com/eb7aff0abd31a7de3397a6caf8f8debe/thumb/1000)
after
- ![image](https://gyazo.com/6feeafba7920b550244aa90d0d3aa7a7/thumb/1000)
    - 2hopリンクが二重になってるのは単純なバグ
- ![image](https://gyazo.com/8bbb2555e05cc52196682f4c5134dea9/thumb/1000)
    - 空のページからは2hopリンクが発生しないのか…
do
- 中身を作ってみる
- ![image](https://gyazo.com/21fcc56e2dfd63118a2b31ca39fb80ca/thumb/1000)
after
- ![image](https://gyazo.com/e529fb4d4750fdff363b53a594e54ac9/thumb/1000)
    - 2hopリンクが発生した
- ![image](https://gyazo.com/1258baeaec252210c06b100e51c064c8/thumb/1000)
    - 英語版と日本語版の両方があるページに関して、それが両方表示されて、ページ間のリンクもマージされている

---
どっちのScrapboxから来たコンテンツかを明示するようにした
- ![image](https://gyazo.com/8d9ef170c10175410b8e85389620d2d1/thumb/1000)
- 機械翻訳した時には「日本語のこのページを機械翻訳したものです」的なことをここに表示したらいい

---
[/villagepump/2022/01/13](https://scrapbox.io/villagepump/2022/01/13)
- 昨日ScrapboxReaderに付けたリンクの機能は色々バグってた
- 複数のプロジェクトのコンテンツを束ねて表示することができるようになった
- プロジェクトAでXからYにリンクはあるがページY自体はなく、プロジェクトBにはページYがあるようなケースで、特に問題なく(プロジェクトの境目を意識することなく)遷移できる
    - でも今は遷移した後リロードしないといけないバグがある
    - Vercelのキャッシュ周りの理解が足りてなさげ

開発日記を井戸端で書くかこっちで書くか少し迷ったけど、こっちで分量を気にせずに書いて、1日の終わりに要約を井戸端に書くくらいがちょうどいいかなと思った

