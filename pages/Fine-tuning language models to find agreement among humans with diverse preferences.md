
> Recent work in large language modeling (LLMs) has used fine-tuning to align outputs with the preferences of a prototypical user. This work assumes that human preferences are static and homogeneous across individuals, so that aligning to a a single "generic" user will confer more general alignment. Here, we embrace the heterogeneity of human preferences to consider a different challenge: how might a machine help people with diverse views find agreement? We fine-tune a 70 billion parameter LLM to generate statements that maximize the expected approval for a group of people with potentially diverse opinions. Human participants provide written opinions on thousands of questions touching on moral and political issues (e.g., "should we raise taxes on the rich?"), and rate the LLM's generated candidate consensus statements for agreement and quality. A reward model is then trained to predict individual preferences, enabling it to quantify and rank consensus statements in terms of their appeal to the overall group, defined according to different aggregation (social welfare) functions. The model produces consensus statements that are preferred by human users over those from prompted LLMs (>70%) and significantly outperforms a tight fine-tuned baseline that lacks the final ranking step. Further, our best model's consensus statements are preferred over the best human-generated opinions (>65%). We find that when we silently constructed consensus statements from only a subset of group members, those who were excluded were more likely to dissent, revealing the sensitivity of the consensus to individual contributions. These results highlight the potential to use LLMs to help groups of humans align their values with one another.
- [2211.15006 Fine-tuning language models to find agreement among humans with diverse preferences](https://arxiv.org/abs/2211.15006)

(DeePL)
- 大規模言語モデリング(LLM)の最近の研究では、出力を原型的なユーザーの嗜好に合わせるために微調整が行われている。この研究は、人間の嗜好が静的で、個人間で均質であることを前提としており、単一の「一般的な」ユーザーに合わせることで、より一般的なアライメントを実現することができる。
- ここでは、[[人間の嗜好の異質性]]を受け入れ、多様な意見を持つ人々が一致を見出すのを機械がどのように支援するかという、異なる課題を検討する。
    - [[人には個性がある]]
- 我々は、700億パラメータのLLMを微調整し、潜在的に多様な意見を持つ人々のグループに対して、期待される賛同を最大化するような文を生成する。
- 人間の参加者は、道徳的・政治的な問題に触れる何千もの質問（例えば、「金持ちに増税すべきか」）に対して意見を書き、LLMが生成した合意候補文の一致度と品質を評価します。
- 次に、個人の嗜好を予測する報酬モデルを学習させ、異なる[[集約関数]]([[社会的厚生関数]])に従って定義されたグループ全体に対する訴求力の観点から、合意文を定量化してランク付けすることを可能にします。
    - [Social welfare function - Wikipedia](https://en.wikipedia.org/wiki/Social_welfare_function)
    - [社会的厚生関数 - Wikipedia](https://ja.wikipedia.org/wiki/社会的厚生関数)
- このモデルは、人間のユーザーによって、プロンプトLLMのものよりも好まれる合意文を生成し（70%以上）、最終的なランキングステップを欠いた、厳しく微調整されたベースラインを大幅に凌駕しています。さらに、我々の最良のモデルのコンセンサス文は、人間が生成した最良の意見よりも好まれている（＞65％）。
- また、グループメンバーの一部のみから無言で合意文を作成した場合、除外されたメンバーの方が反対意見が多くなり、個人の貢献度に合意文が左右されることが明らかになりました。これらの結果は、LLMを利用して、人間集団が互いに価値観を合わせることを支援する可能性を示しています。
