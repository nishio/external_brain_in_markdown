---
title: "DSPy"
---

2025-04-13
[[LLMの自己改善的なプロンプト最適化]]
<img src='https://scrapbox.io/api/pages/nishio/GPT-4.5/icon' alt='GPT-4.5.icon' height="19.5"/>
2025年現在、LLM自身がプロンプトを自動改善する手法（DSPy的なアプローチ）は以下のような進展を見せています。

- DSPyのその後の発展
    - DSPyはプロンプト改善を自動化する仕組みだが、さらに[[自己反省]]・[[自己修正]]を取り入れた「[[Self-Refine]]」「[[Reflexion]]」などが登場。
    - モデルが自分で回答を評価して改善案を考えることで、性能を大きく向上させた。

- 自己反省・自己修正の限界
    - 自己修正プロンプトは有効だが、モデルが自身の誤りを見つけるのは容易ではなく、逆に性能が悪化することもある。
    - そのため、外部情報（検索エンジン等）や強化学習を活用してフィードバックを補強する研究が進んでいる。

- 自己強化学習の活用
    - 自分の回答にフィードバックを与え、そのデータを自己生成して微調整する手法が広まる（例：[[GoogleのSCoRe]]）。
    - Metaなどはモデルに自己評価の仕組み（ジャッジ）を持たせ、追加の人間評価なしに性能向上を達成。

- 実用化の状況
    - DSPyはすでに企業で実用化され、プロンプト調整の手間を大幅に削減。
    - 商用LLMにも自己改善や自己修正能力が徐々に組み込まれ始めている。

今後もこの「モデル自身が学習して改善する」という方向性は注目され、外部連携や自己評価の高度化によって、さらに発展すると予測されています。

---
2024-05-02
[[stanfordnlp/dspy]]は[[自動プロンプトエンジニアリング]]の有望なアプローチであり、将来的なLMプログラミングの方向性を示唆していると言えます。<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>

<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/><img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
DSPyとは
- 言語モデル (LM) を使ったパイプライン構築のためのPythonフレームワーク
    - 宣言的なモジュール定義
    - モジュールの合成によるパイプライン構築
    - 自動的なプロンプト最適化

DSPyの基本概念
- パイプライン
    - パイプラインは、モジュールを組み合わせたワークフロー
    - あるモジュールの出力を、別のモジュールの入力として接続することで、複雑なタスクを達成します
- モジュール
    - モジュールは、LMの呼び出しを抽象化した部品
- シグネチャ
    - シグネチャは、モジュールの入力と出力のインターフェース
- コンパイラ
    - コンパイラは、パイプラインを最適化する
    - 各モジュールに対して、最適なプロンプトを生成したり、パラメータを調整したりすることで、パイプライン全体の性能を向上させます

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
具体的にはチュートリアルだとこんなシグネチャが出てくる
python

```
class BasicQA(dspy.Signature):
    """Answer questions with short factoid answers."""

    question = dspy.InputField()
    answer = dspy.OutputField(desc="often between 1 and 5 words")
```

これは内部でTemplateと呼ばれるものに変換されててこんな感じになる
py

```
(Pdb) print(template)
Template(Answer questions with short factoid answers., ['Question:', 'Answer:'])
```

これが__call__をもってるのでexampleを渡す
py

```
(Pdb) print(example)
{'demos': [], 'question': 'What is the nationality of the chef and restaurateur featured in Restaurant: Impossible?'}

(Pdb) print(template(example))
Answer questions with short factoid answers.

---

Follow the following format.

Question: ${question}
Answer: often between 1 and 5 words

---

Question: What is the nationality of the chef and restaurateur featured in Restaurant: Impossible?
Answer:
```


exapmle.demosに事例を追加するとこうなる
py

```
(Pdb) example.demos.append({"question": "SAMPLE_QUESTION", "answer": "SAMPLE_ANSWER"})
(Pdb) print(template(example))
Answer questions with short factoid answers.

---

Follow the following format.

Question: ${question}
Answer: often between 1 and 5 words

---

Question: SAMPLE_QUESTION
Answer: SAMPLE_ANSWER

---

Question: What is the nationality of the chef and restaurateur featured in Restaurant: Impossible?
Answer:
```


これが「プロンプトを生成」
では「自動的なプロンプト最適化」とは何か
一番シンプルな例としてチュートリアルではこんなことをしている
py

```
teleprompter = BootstrapFewShot(metric=validate_context_and_answer)

# Compile!
compiled_rag = teleprompter.compile(RAG(), trainset=trainset)
```


BootstrapFewShotとは先ほどのexapmle.demosに何を載せるかを決めるもので、中でLabeledFewShotを呼び出してtrainsetからランダムにk個選んでいる
- リポジトリにはbayesとかoptunaとかある

demosに使わなかったもので正解率を計算(これは上記のmetricで評価関数を外から渡してる)
正解率の高かったものを選ぶ、これを「compile」と読んでいる。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/><img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>
この一連の処理を"コンパイル"と呼んでいます。つまり、プロンプトを一種の"機械語"とみなし、それを最適化するプロセスをコンパイルと捉えているのです。

この考え方は、プログラミング言語の歴史において[[C言語]]が登場したことと類似しています。C言語は、様々なアーキテクチャに対してコンパイルできる[[高級言語]]として、プログラミングを大幅に効率化しました。同様に、DSPyのようなフレームワークは、様々なLLMに対して最適なプロンプトを自動生成することで、LMを使ったアプリケーション開発を効率化する可能性を秘めています。

ただし、DSPyが新たなC言語になるかどうかは現時点では不明確です。結局のところ、泥臭くても実用的なものがデファクトスタンダードになる傾向があります。(追記: [[FORTRAN]]が登場した時にはコンパイルのことが[[自動プログラミング]]と呼ばれてた。その後、後発のC言語がシェアを奪った)

また、DSPyを使う上での課題として、評価関数(metric)の定義が挙げられます。タスクごとに適切なmetricを定義することは容易ではありません。顧客のニーズを、metricの定義が容易なタスクに分解するスキルが求められるでしょう。
metricの定義自体にLMを使うことも考えられますが、繰り返し実行回数が多いため、最適化の圧力が高くなります。そのため、既存の自然言語処理の知識を活かした効率的な実装が必要になるかもしれません。

総じて、DSPyは自動プロンプトエンジニアリングの有望なアプローチであり、将来的なLMプログラミングの方向性を示唆していると言えます。一方で、実用上の課題もまだ多く残されています。DSPyやその他のフレームワークがどのように発展していくのか、注目が集まります。

関連
- [[LLMの更新とニーズの境目]]
