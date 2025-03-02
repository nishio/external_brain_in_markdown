---
title: "GPT-3"
---

Playground
- [https://platform.openai.com/playground](https://platform.openai.com/playground)


[https://beta.openai.com/docs/introduction/overview](https://beta.openai.com/docs/introduction/overview)
- fine-tuningも出来るのか！！<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
- `completions endpoint`
    - 「質問して思考を促すチャットボットの名前を提案して」と言ったらソクラテス(Socrates)っぽい名前を選んだ、すごいな
        - ![image](https://gyazo.com/3a232960e15c26c22a49d758bf3225fd/thumb/1000)
    - 日本語で聞いてみよう
        - ![image](https://gyazo.com/97e9d512df9f5a0ec258e4a1ab7e0598/thumb/1000)
    - あーなるほど、質問に答えてるのではなく続く文章の生成をしてるのか
        - ![image](https://gyazo.com/1e6c117a7080dc0c979bd3a785b04d8a/thumb/1000)
    - Curious Catいいな
    - 日本語話者向けの名前を出せるかな？
        - ![image](https://gyazo.com/86def19fb9b4741c4b7753460d2edddd/thumb/1000)
    - 候補はイマイチだけど、ちゃんと「日本語話者向け」って指示を理解しているな
    - 「今の名前はKeichobot。これは「傾聴」由来です。」
        - ![image](https://gyazo.com/4b9ce54d3010ffe72d17b8ffea0a7222/thumb/1000)
    - 「えーと」ってww
    - しかしちゃんと「話を聞くって特徴を使う方がいいのだな」と読み取ってる、ほんとすごいなこれ
    - 温度を上げるとランダムさが上がる、たくさん候補を出して選びたい時には良い
        - ![image](https://gyazo.com/9a41f673c32e7f753d10bf827c614e03/thumb/1000)
        - ![image](https://gyazo.com/472d3a68323ffe288350df77e9f089a9/thumb/1000)
        - みつけぼっと、いいな
            - いまの「傾聴ぼっと」も自分は「けいちょぼっと」みたいな発音してるし、3モーラであることを無意識に好んでたのかも
        - 「〜ラボ」ってのも、今回考えてたものとはちょっと違うけど、別バージョンの「情報が蓄積していって、過去の会話ともリンクするシステム」の名前としては面白げ
            - 「きづきラボ」とか
- あれー、他のモードの説明なしにコードを書く話になってしまった
    - インストラクションと入力があるタイプのタスクはどうするのかな
    - 単に結合してるだけなのかな
        - ![image](https://gyazo.com/6a3b8ebd081ea624c8050d8c4ea6b621/thumb/1000)
    - そういうことみたい
        - ![image](https://gyazo.com/c84e778d970de5f4b8ff7b6fa0aa8b23/thumb/1000)
    - 適切なキーフレーズを選択してそれを掘り下げる質問をせよ
        - ![image](https://gyazo.com/336666b3aef107350c54ce28e04ad67a/thumb/1000)
    - 質問は正しく作れてる！
        - 解答は作らなくていいんだよ…
    - ![image](https://gyazo.com/29a55ee2170c85b9c0db012e69d774ca/thumb/1000)
        - うーん
    - ![image](https://gyazo.com/f1503fd802a572d4dbba40f1bd594402/thumb/1000)
    - ![image](https://gyazo.com/e29ddfc0cd95a50ab463925705184283/thumb/1000)
    - ![image](https://gyazo.com/0377b17e5bae715d0f1e411ed4592b7b/thumb/1000)
    - うーん、さっきはうまく質問できてたのに…たまたまなのかな…
    - ![image](https://gyazo.com/5c608677bfa32b88e9d63d2e60edbb7d/thumb/1000)
    - ![image](https://gyazo.com/a74431dc374dcade31b75361c7fadfbd/thumb/1000)
    - ![image](https://gyazo.com/174b5d3e5addc9de13bdd90072e9db6f/thumb/1000)
    - うーん。日本語で質問文を作れという指示が理解してもらえない。出てきた質問文を別途翻訳したりすると「頭がスッキリするといい」「頭がクリアになるとはどういうことですか？」みたいなやりとりになるから相手の発言からキーフレーズを拾って掘り下げ質問をするって目的が達成できない…
