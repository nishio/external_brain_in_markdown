
from [/villagepump/Kozaneba+Scrapbox](https://scrapbox.io/villagepump/Kozaneba+Scrapbox)
<img src='https://scrapbox.io/api/pages/villagepump/nishio/icon' alt='/villagepump/nishio.icon' height="19.5"/>
- ScrapboxのカードをKozanebaで整理することをしたい/やってる人が複数人いる
- [[Scrapboxベストプラクティス2022原稿v1]]でもScrapbox上で行われた多人数の議論をKozanebaで整理した
- Scrapboxとの親和性を高めていこう
    - それにはScrapboxのプロジェクト名が必要になる
        - アイコン記法の画像での表示
        - リンク記法で書かれてるものを実際にリンクにする
    - これは前々からわかっていた
        - が「他サービスと密結合な機能を入れるのは良くないのでは？」と考えてこの方向に進むことを躊躇っていた
- 未踏会議2022での村井純先生の話
    - > インターネットは電話線に対するオーバーレイネットワークとして生まれた
    - >  そしてその有用性が広く知られ広く使われるようになってから下部レイヤーが交換された
    - この話を聞いて、確かにそれが良いのかもなと思った
- つまりScrapboxをインフラとし、それに対するオーバーレイとしてKozanebaを使えるようにする。
    - それによって有用性が理解され使われるようになってから下部レイヤーを交換できるようにする
    - 「インフラとする」の概念は曖昧
        - まずは「Scrapboxからデータを取ってきて整理」「整理したものをScrapboxに反映」のコストを下げて使いやすくする感じかな


- マップに「Scrapboxのプロジェクト名」フィールドを作る
- これが空文字列でないなら、こざねのテキストはScrapbox記法としてパースする
    - リンクとかアイコンとか
    - アイコン記法はアイコンとしてこざねに埋め込む
    - 画像記法は画像こざねになればいい
    - Scrapbox記法のリンクは
            - 別タブで開く
            - こざねとして追加する
        - を選択できるといい？
            - こざねとして追加する
                - これをしたらScrapboxこざねからopenはできるからそれでいいかも
    - リンクをたどりながらScrapboxのページをKozanebaにどんどん追加していける

<img src='https://scrapbox.io/api/pages/villagepump/nishio/icon' alt='/villagepump/nishio.icon' height="19.5"/>
- Scrapboxで始まるよりKozanebaで始まる方がリンクサジェストの確定が早いので変えた


2022/3/24
- ![image](https://gyazo.com/161582ef0cc55da4a64a3e8b5f18d64f/thumb/1000)
- ✅マップに「Scrapboxのプロジェクト名」フィールドを作る
    - これが空文字列でないなら、こざねのテキストはScrapbox記法としてパースする
        - リンクとかアイコンとか
        - アイコン記法はアイコンとしてこざねに埋め込む
- 🤔Scrapbox記法のリンク
    - これをDOM的にもリンクにしてしまうと操作しにくくなる気がした
