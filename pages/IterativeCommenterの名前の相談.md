---
title: "IterativeCommenterの名前の相談"
---

from [[日記2023-09-04]]
IterativeCommenterの名前の相談

実装の変更:
- URL指定で読んでコメントする時、下に書くほうが自然
- 下に書くようにすると前回のノートの取得も変える必要がある
    - どうあるべきなんだ？
    - 冒頭部をサマリーとし、下を会話スペースとする設計を想定してたけど、そうなると人間が上のサマリーを更新しない限り入力が変化しないな
        - まあ[[ページメモリ]]で見る断片が変わっていったり、他の新しい断片が追加されてそれを拾ったりするからいいのか？
        - 元々の[[Recurrent Notes]]みたいに話題が明後日の方向に転がって行くことはなくなる代わりに、冒頭部にあるサマリーの周辺に留まって徐々に外側に探索して行くようになる
        - それはそれで有益な気がするな
        - キャンプから周辺を探索し、有益なところが見つかったらキャンプを移動

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>かつてAIがノートAを書いて、翌日にAを読んでBを書く、という繰り返しのシステムを作ってrecurrent_notesと呼んでいた。少し変更して、AIはあるページの冒頭部を読み、ページの末尾にコメントを追加するようになった。この時冒頭部には人間の手による要約が置かれて、AIの出力は人間の手を介さなければ次回の読む対象にはならなくなった。このシステムの名前はなんとするのが適切か？

<img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>「recurrent_notes」の原理を基にして、AIがページの冒頭部を読み、ページの末尾にコメントを追加するという新しい形に変わったシステムに関して、名前を考えるとなると、以下のような提案が考えられます：
- [[Iterative Commenter]]（繰り返しコメント者）：「繰り返し」という意味の"iterative"と、コメントを追加する動作を指す"commenter"を組み合わせた名前です。
- PageTailor（ページカスタマイザー）：ページの「末尾」にコメントを加える機能を指す"tailor"（調整する、カスタマイズする）と組み合わせた名前です。
- SummaryResponder（要約に応答者）：ページの冒頭の「要約」に基づいてAIがコメントをするので、それを表現する名前です。
- [[NoteReflector]]（ノートの反映者）：既存の内容に基づいて新しいコメントや反応を生成するという点から、"reflect"（反映する）の概念を取り入れた名前です。
- FeedbackLoopNotes（フィードバックループノート）：繰り返しのフィードバックループの考えを取り入れ、元の「recurrent_notes」との関連性も感じられる名前です。
最終的には、システムの目的や特徴、利用シーンなどを考慮して、一番適切と感じる名前を選ぶのが良いでしょう。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>IterativeCommenterは素朴に振る舞いを記述してる感がある。NoteReflectorはかっこいいけどReflectの熟考のニュアンスが伝わりにくいかな？

<img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>確かに、名前の選択はそのシステムの性質や目的、そして対象とするユーザー層や文化的背景に応じて異なる印象を持つことがあります。また、名前の単語やフレーズが持つニュアンスや意味合いも重要です。
「IterativeCommenter」は、システムの動作を直接的に反映しているので、機能的でわかりやすい名前と言えます。一方、「NoteReflector」は少し抽象的であり、熟考や深い反映を意味する「reflect」のニュアンスが完全に伝わらない可能性があります。

これを考慮すると、以下のような名前も考えられます：
- NoteAugmenter（ノート増強者）：元の内容に基づいてコメントを追加することで情報を増強するという意味合いを持つ。
- PageAmplifier（ページ増幅者）：ページの内容を強化・増幅するという意味合い。
- ContentEnhancer（コンテンツ強化者）：要約に基づくコメントで全体のコンテンツの価値を強化する概念。

どの名前が最も適切かは、システムの全体的なコンセプトやブランディング、ターゲットユーザー層のニーズや期待によって異なります。上記の提案を基に、さらにアイデアを練り直しても良いかと思います。

---
[[Reflection]]
