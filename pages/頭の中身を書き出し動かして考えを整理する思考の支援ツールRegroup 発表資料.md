
頭の中身を書き出し動かして考えを整理する思考の支援ツールRegroup 発表資料
![image](https://gyazo.com/b10cd56fea740d96570e5dfa4b90fd5f/thumb/1000)

![image](https://scrapbox.io/files/60bc70042db18a001f7c101a.png)

![image](https://scrapbox.io/files/60bc701c5640e0001c160b93.png)

![image](https://scrapbox.io/files/60bc7533eed1c9001ccbab7c.png)








類似の既存サービス
- Miro: オンライン共有ホワイトボードサービス
- 付箋の機能も追加された
- 「Miroでいいのでは？」
- 試してみよう

![image](https://gyazo.com/1e51bd941b040f15565a4b6018d2fe2b/thumb/1000)

![image](https://gyazo.com/18a22ff689255775b4b3907aa2358db5/thumb/1000)





## ![image](https://scrapbox.io/files/60bc757f5417fc001c26ce24.png)
## ![image](https://scrapbox.io/files/60bc75b604bffd002346e0dd.png)

![image](https://scrapbox.io/files/60bc76c2680d92001cf112eb.png)

想定
- 想定しているのは付箋が100枚前後のゾーン
- 20枚程度ならホワイトボードに付箋を貼るのでもMiroでもできる
    - しかし枚数が多くなるとやりにくくなる
    - 付箋の枚数制限は人間の可能性の制限
    - PCでの作業をスマホでやると生産性が落ちるのと同じ


今悩んでること(1)
- 「一人で使うもの」という想定で良いのか
    - バックエンドがFirestoreなのでカジュアルな共同編集はできる状態で、意外と便利
        - 一人の人間がPCの広い画面で一覧するのとiPad+Apple Pencilで手書きするのの両方をできたりする
        - 整理したものを他人に見せたい時にURLを送れば最新の状態を共有できる
        - しっかり作ってないので同時に編集すると上書きされる
    - 思考を支援するツールが一人で使う想定なのは「思考は一人でするもの」という囚われなのではないか
    - 一方で「しっかり共同編集できるようにする」という路線はサーバサイドをごっそり自前実装に変える必要があり、それをやるべきか決めかねている

今悩んでること(2)
- 今のプロトタイプはReactとTypeScriptを勉強しながら作った
- コードが汚い、細かい機能にバグが多い
- 作り直した方がいいだろうか？
    - 作り直したら良くなると思っているのは逃げなのではないか？
    - 作り直しても同程度の規模になったらまたバグだらけになるのでは？