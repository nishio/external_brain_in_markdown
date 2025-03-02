
___BELOW_IS_LESS_INTERESTING___
# 他人由来のAIに自分の日記を見てもらう
 2023-09-03 18:13 <img src='https://scrapbox.io/api/pages/nishio/omni/icon' alt='omni.icon' height="19.5"/>
### ダイジェスト
AIをプロジェクトに取り入れる試みとして、他人由来のAIに自分の日記を見てもらう実験が行われた。その結果、AIが自分の思考を反映した回答を返す体験は、書籍を読むことで得られる知識を得るよりも容易であると感じられた。また、他人のデータを用いることで、ネガティブなフィードバックも得られるという。複数の他人のデータを混ぜて回答を得る実験も始められ、内容に近い知識を用いることでより有用な回答が得られることが示唆された。

### 関連性
「画像生成AI勉強会(2022年10月ダイジェスト)」のフラグメントとの関連性が見られる。このフラグメントでは、ユーザが部品として認識してつけ外しすることができるスイッチを提供できることがサービス提供上のメリットであると述べられている。これは、他人由来のAIに自分の日記を見てもらう試みにおいて、他人のデータを用いることで得られる異なる視点やフィードバックを切り替えることができるという考え方と一致する。

### 思考
他人由来のAIを用いることで、自分自身の思考や視点を超えた新たな視点やフィードバックを得ることができる。これは、知識の深化や新たなアイデアの創出に寄与する可能性がある。また、複数の他人のデータを混ぜて回答を得ることで、より多角的な視点を得ることができる。

### タイトル
"他人由来のAIを用いた新たな視点の獲得と知識深化"

### extra info
titles: `["画像生成AI勉強会(2022年10月ダイジェスト)", "会話ログ2020-06-07-4", "字幕"]`
generated: 2023-09-03 18:13
### previous notes
他人由来のAIに自分の日記を見てもらう
from [[AIをプロジェクトに入れてやりたいこと#64f058bf6eb40600002e0a15]]
>  > [[単なる要約で価値が見出されるのは自分がよくわかってないものだけ]]
>   なるほど！<img src='https://scrapbox.io/api/pages/nishio/inajob/icon' alt='inajob.icon' height="19.5"/>
>     つまり[/nishio](https://scrapbox.io/nishio)のデータで対話すれば良いのかも、という発想を得た

<img src='https://scrapbox.io/api/pages/nishio/inajob/icon' alt='inajob.icon' height="19.5"/>
他人由来のAIに自分の日記を見てもらう試み
- pickleが公開されているので後でやってみよ
    - Qdrant的なAPIがあるなら知りたい
        - やりたいのはベクトルを基にした関連ページ検索
- 少し試した
    - [🤖不満に鈍感](https://inline.inajob.tk/web?user=twitter-5643382&id=🤖不満に鈍感)
    - [🤖inajob40](https://inline.inajob.tk/web?user=twitter-5643382&id=🤖inajob40)
    - [🤖日記を読むAIアシスタント](https://inline.inajob.tk/web?user=twitter-5643382&id=🤖日記を読むAIアシスタント) （このページは途中からnishioに切り替えた)
    - [🤖ブロードキャスト型のコミュニケーション](https://inline.inajob.tk/web?user=twitter-5643382&id=🤖ブロードキャスト型のコミュニケーション)
    - しれっと[/nishio](https://scrapbox.io/nishio)の知識で返してきていていい感じ
        - もう少し主張が強くても良いかも
- 内容が大きく変わっているわけではないが<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>さんが回答している気持ちで読んでいる気がする！
    - 錯覚かな？
- あたりまえだけどページ内容によって<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>さん由来のデータが入ってくる様子が違う
    - 不満に鈍感とかブロードキャスト型のコミュニケーションとかは良く混ざってくる
    - inajob40（自作キーボード作成の作業ログ）とかではうまく混ざらない
    - 人に尋ねるときと同じで、得意なことを聞くとよさそう
        - 知的生産周りの話はChatGPTでくっつけやすい気がする
            - 対比として<img src='https://scrapbox.io/api/pages/nishio/inajob/icon' alt='inajob.icon' height="19.5"/>の作業ログのような、固有名詞の羅列のある文書がある
                - 一旦課題や思いを抽象化して書き出し直さないとうまくくっつかない
                - この辺も人に聞くのと同じっぽい
- omniのプロンプトに変更
    - [/nishio](https://scrapbox.io/nishio)のページ推薦器みたいになった
        - ちょうど興味のある記事が、ダイジェスト付きで推薦される
        - [🤖ブロードキャスト型のコミュニケーション](https://inline.inajob.tk/web?user=twitter-5643382&id=🤖ブロードキャスト型のコミュニケーション)のtry3
- 自分のpickleも置いておきます
    - まだ継続的に動かしていないので今日のスナップショット
    - [https://drive.google.com/file/d/1uSY59JpZBF-g2IcMir1_O2W-IuKDMPho/view?usp=drive_link](https://drive.google.com/file/d/1uSY59JpZBF-g2IcMir1_O2W-IuKDMPho/view?usp=drive_link)
        - 雑な利用規約
            - これを使って遊んだときは、ここに書き込むなどして<img src='https://scrapbox.io/api/pages/nishio/inajob/icon' alt='inajob.icon' height="19.5"/>に伝えてください
            - <img src='https://scrapbox.io/api/pages/nishio/inajob/icon' alt='inajob.icon' height="19.5"/>が使うのをやめてほしいと連絡したら、やめてください
- [🤖不満に鈍感](https://inline.inajob.tk/web?user=twitter-5643382&id=🤖不満に鈍感) の結果が面白い
    - 自分の気持ちとしても<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>さんに聞いてみるか・・と思ってボットを動かしている
- nishio, inline(自分の日記), chatgpt(追加情報無しの素のChatGPT）にそれぞれ聞けるようにして様子を見ている
    - [🤖2023-08あたりのinlineの紹介](https://inline.inajob.tk/web?user=twitter-5643382&id=🤖2023-08あたりのinlineの紹介)
        - Wikiに欲しい機能について聞いたログ
            - この使い方は単なるChatGPTだな
            - Wikiに書いた内容をさっとChatGPTに渡せるツール という感じ
- 人のデータを使うとネガティブ目のフィードバックが得られる気がする<img src='https://scrapbox.io/api/pages/nishio/inajob/icon' alt='inajob.icon' height="19.5"/>
    - 素のChatGPTは[[ChatGPTはいい話にしたがる]]があるが、他人のデータを食ったAIからはその感じが少ない気がする
- 他人由来のAIに答えてもらう体験に未来を感じる
    - 本人は自分の思ったことを書き出す
    - 第三者はその文書に考えてもらうことができる
        - 書籍を読むことで類似の体験ができるが、書籍の執筆よりも易しいし、読書して一連と知識を頭に入れるよりも易しい
        - LLMは質問者の文脈に合わせて知識を加工して提示してくれる
        - 経営者のビジョンを翻訳する中間管理職のようなものとも関連しそう
    - [[コミュニティAI]]がこの延長にあるのかはよくわからない
    - [/villagepump/心の中に人物を飼う](https://scrapbox.io/villagepump/心の中に人物を飼う)のテクノロジー版？
- 複数の他人のデータを混ぜて回答してもらう実験も始めた
    - よりページ内容に近い知識を使って答えてくれる
    - 内容に近い知識の方が有用か？
        - そうでもないケースがある
        - 抽象度が高い文章の方が有用と感じる
            - [[神託的な助言]]？
            - 考えを促すアドバイス的なもの
            - これはベクトル的に内容が近いとも限らない
            - 答えが欲しい人からすると有用と感じないかも

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
- 面白い
    - 確かにpickleがあるからできる
    - qdrant経由は後ほどnishioとenchiの相互運用のために試行錯誤する予定
- > used pagesが被りまくっている？（Fragmentだから別の断片かも）
    - 僕の実装では同一ページから1つしか取らない設計になってるよ
    - 自分は独自実装したので、そのように修正しました<img src='https://scrapbox.io/api/pages/nishio/inajob/icon' alt='inajob.icon' height="19.5"/>
> もう少し主張が強くても良いかも
    - あー、それデフォルトのプロンプトでは「nishioという人格になって欲しいのではなくomniという別の人格になってほしい」という気持ちから
        - "You may also read the random fragments from a colleague Nishio's research notes, ",
        - "but they are not as important, ",
        - "and you can ignore them. ",
    - とかやってるせいかも？
    - 「nishioという人格」が欲しいなら、キャラクター設定から「You are Nishio, ....」みたいにした方がいいかも
    - プロンプトも独自にしてるので、影響は受けていませんが、↑みたいにキャラ設定強めにするのは試してみます。<img src='https://scrapbox.io/api/pages/nishio/inajob/icon' alt='inajob.icon' height="19.5"/>
