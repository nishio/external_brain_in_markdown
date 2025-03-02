
[https://github.com/compdemocracy/polis/discussions](https://github.com/compdemocracy/polis/discussions)

[Would you approve CORS requests so that an approved group could build a custom frontend? · compdemocracy/polis · Discussion #1680 · GitHub](https://github.com/compdemocracy/polis/discussions/1680)
- "No, make own instance"

[Divisiveness/consensus metric in automatic report · compdemocracy/polis · Discussion #1661 · GitHub](https://github.com/compdemocracy/polis/discussions/1661)
- "divisiveness" = "extremity"
- [[Polis: Scaling Deliberation by Mapping High Dimensional Opinion Spaces]] p.9-10
- ちょっとよくわからないが今は必要でないのでスキップ

[Improving the moderation workflow in large conversations · compdemocracy/polis · Discussion #1551 · GitHub](https://github.com/compdemocracy/polis/discussions/1551)
- モデレーションをしないスタイルは後から参加する人の経験を損ねる
- モデレーションがしんどい、改善が必要
    - 投稿された意見を編集して承認する機能
- モデレーションの透明性を担保する必要がある
- 「反対意見は通常必要ない」
    - 「これはもっと議論した方がいい」
        - 両サイドの意見があった方がいい
            - グループを「反対している」で特徴づけるより「賛成している」で特徴づける方が理解しやすい説
        - 量が多くなる
            - 発言を節約する
    - 意見モデレーション画面がページネーションのない新着100件だったのでモデレーションできなくなった問題
- 重複排除を容易にするために発言をトピックごとに分類する
    - これは埋め込みベクトルの類似度で判断できるかもね<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
        - もしくは、投票を負担に感じてないユーザが10〜20人程度いれば、そのユーザに先に投票させ、その投票結果のベクトルが既存の意見のベクトルと独立性が低いなら(新しい情報を提供する可能性が低いなら)無視するという選択肢が考えられる
        - これは既存の「Priority」メカニズムとも関係するかもしれない
    - 書いた

[Why is there 109 people voted but only 49 grouped? · compdemocracy/polis · Discussion #1528 · GitHub](https://github.com/compdemocracy/polis/discussions/1528)
- > Participants have to vote a minimum of 7 times to be included.


[Accessing the pol.is vizualization · compdemocracy/polis · Discussion #1282 · GitHub](https://github.com/compdemocracy/polis/discussions/1282)
- コメントそのものが2次元平面にどのように埋め込まれるか
- > In short, the comments are projected as though they were a participant who voted on only the comment in question. So in effect, they're just projected according to the PC loadings, scaled by the same factor applied towards participant projections, so that they can be more easily plotted together.
    - 要するに、あたかも当該コメントのみに投票した参加者であるかのように投影しているのです。つまり、実質的には、PCの負荷量に従って投影し、参加者の投影に適用されるのと同じ係数でスケーリングして、より簡単に一緒にプロットできるようにしているだけなのです。
- 数学
    - [Conversa Polis User Group open calls - HackMD](https://hackmd.io/@patcon/conversa-calls/https%3A%2F%2Fhackmd.io%2F%40patcon%2Fr1KpFakV_)
        - モデレータービューには投票が付随しない
            - 熱心な参加者が自分以外のグループの賛成を引き出したい場合、暗黙のうちに+1されることを知っているなら否定形で書く必要がある
        - “not not A != A”
        - レポートページでのみGPT-3で肯定的文言に変換するのを試している
            - GPT APIが個人的なものなのでオプションにする必要がある
        - PCAをしてから距離を計算している、なぜ？情報を捨てているのでは？
            - PCAがノイズ除去として機能する
            - 2次元可視化に役立つ情報にフォーカスしてる
            - でも3次元以上で起こってることを見落としたくないでしょ？
            - [[利用と探索のトレードオフ]]のようだ
            - PCAのトップ4次元を取り出してそれぞれの2Dプラットを作ったが意表をつく相関があった
- > I started a version to show how groups are created and comment chosen according to the original paper, however, not all of the methodology is clear to me from
    - [Group creation and representative comment selection by chrvt · Pull Request #4 · compdemocracy/analysis · GitHub](https://github.com/compdemocracy/analysis/pull/4)

