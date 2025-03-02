---
title: "オーケストレーション層の入ったAIと話す"
---

> [nishio](https://x.com/nishio/status/1878660926154662108) ふと思ったんだけど[[オーケストレーション層]]の入ったAIと話す時って、今までのシンプルなAIと話す時みたいに「指示」するのではなく、「目的」を伝えてどうやって実現するかはAI自身に考えさせた方が良いんじゃないか？(人間をマイクロマネージするかどうかみたいな話になってきたぞ？)
> [cactaceae](https://x.com/cactaceae/status/1878661144472408307) o1向けプロンプトガイドがそんな話してた気がする
> [nishio](https://x.com/nishio/status/1878665078477819947) 情報ありがとうございます！見てみます！

> [teramotodaiki](https://x.com/teramotodaiki/status/1878662902032539944) まさに人間のマネジメントと同じで、結局はDevinにどこまでの裁量を与えられるか次第だと思います
>  例えば、
>  ・振る舞いを変えて良いか
>  ・新しいパッケージを入れて良いか
>  ・プルリクをマージして良いか
>  など。何でもやって良いならゴールを与えるだけでよく、制約が多いならタスクを渡した方がよい
> [nishio](https://x.com/nishio/status/1878665444275744815) Devinを触っていくうちに、ChatGPTのo1と話す時と4oと話す時は話し方を変えるべきでは？と思ったという話で、実際プロンプトガイドにそんなことが書いてあるらしいので読んでみます

公式ドキュメントはマイクロマネジメント的なことを言ってる
- [Reasoning models - OpenAI API](https://platform.openai.com/docs/guides/reasoning/advice-on-prompting)
    1. 明確で具体的な指示を与える
        - モデルに対して曖昧な指示を避け、具体的で明確なタスクを提示することが重要です。例えば、「以下の文章を要約してください」ではなく、「以下の500語の技術記事を100語以内で要約してください」と指定すると、より適切な出力が得られます。
    5. 複雑なタスクはステップに分解する
        - 複雑な問題やタスクは、モデルが処理しやすいように小さなステップに分解して指示します。例えば、「まずデータを分析し、その後、結果をグラフ化してください」と段階的に指示すると、より正確な結果が得られます。

o1はDevin的な意味でのオーケストレーション層があるわけではなく[[Chain of Thought]]をがっつりやってるだけだからか
- なので[[ツール利用]]であるネット検索などができない
- Devinはo1とはまた違った方向の能力を獲得している

そんなことより3ヶ月前に更新されてる[Best practices for prompt engineering with the OpenAI API | OpenAI Help Center](https://help.openai.com/en/articles/6654000-best-practices-for-prompt-engineering-with-the-openai-api)を見てたら知らない機能が書いてあった
9. Use the [[Generate Anything feature]]
