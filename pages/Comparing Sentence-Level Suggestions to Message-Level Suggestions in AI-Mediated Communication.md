
> Traditionally, writing assistance systems have focused on short or even single-word suggestions. Recently, large language models like GPT-3 have made it possible to generate significantly longer natural-sounding suggestions, offering more advanced assistance opportunities. This study explores the trade-offs between sentence- vs. message-level suggestions for AI-mediated communication. We recruited 120 participants to act as staffers from legislators’ offices who often need to respond to large volumes of constituent concerns. Participants were asked to reply to emails with different types of assistance. The results show that participants receiving message-level suggestions responded faster and were more satisfied with the experience, as they mainly edited the suggested drafts. In addition, the texts they wrote were evaluated as more helpful by others. In comparison, participants receiving sentence-level assistance retained a higher sense of agency, but took longer for the task as they needed to plan the flow of their responses and decide when to use suggestions. Our findings have implications for designing task-appropriate communication assistance systems.
- [https://dl.acm.org/doi/10.1145/3544548.3581351](https://dl.acm.org/doi/10.1145/3544548.3581351) (2023)
- (DeepL) 伝統的に、文章作成支援システムは、短い、あるいは単一単語の提案に焦点を当ててきました。近年、GPT-3のような大規模な言語モデルにより、かなり長い自然な響きの提案を生成することが可能になり、より高度な支援の機会が提供されるようになった。本研究では、AIを介したコミュニケーションにおける文レベルの提案とメッセージレベルの提案のトレードオフを探る。我々は、大量の有権者の懸念に対応する必要があることが多い議員事務所のスタッフとして120人の参加者を募集した。参加者は、さまざまなタイプの支援メールを返信するよう求められた。その結果、メッセージレベルの提案を受けた参加者は、主に提案された原稿を編集したため、返信が早く、その経験により満足していることがわかった。加えて、彼らが書いた文章は、より役に立ったと他者から評価された。それに比べ、文章レベルの助言を受けた参加者は、より高い主体性を保持したが、回答の流れを計画し、いつ助言を使用するかを決定する必要があったため、タスクに時間がかかった。この結果は、タスクに適したコミュニケーション支援システムの設計に示唆を与えるものである。

細かい単位で生成して組み合わせるより、まとめて全体を生成する方が意外といいものの出てきて作業時間が省ける〜というGPTを使い倒してる人なら肌感として知ってることを実験で確認したもの。GPT3の時代の実験。
- > Generation model. We use GPT-3 (specifcally, the text-davinci002 model without any fine-tuning) to generate suggestions.

興味深いのはここ
- ![image](https://gyazo.com/6423b49cef438875e16d40b1a7903932/thumb/1000)
- (GPT3.5) 図9: メッセージレベルの提案を用いて書かれた応答は、文レベルの提案やAI支援なしで書かれた応答よりも有意に役立つと評価されました。各データポイントごとに500回の判断が行われました。エラーバーは95％信頼区間を示しています。Y軸は、X軸に表示される応答のタイプに応じて参加者が評価した応答の平均的な役立ち度を示しています。AIの関与を明示的に示した応答は青で色分けされています。

- 作ったメッセージを、別の人900人に見せて役立ち度合いを評価させる実験をしている
    - GPTがメッセージ全体を生成して人間が手直ししたものは、生身の人間が独力で書いたものより役立ち度が高い
        - AIの支援を受けていることを開示すると役立ち度の評価は下がるが、それでも生身の人間が書いたものより評価が高い
    - AIで生成して人間の関与なしに送ったものですら開示なしだと人間より評価が高い
        - 既存の自動返信に比べると格段に良い

この結果が`text-davinci002 model without any fine-tuning`で得られているのがすごい
