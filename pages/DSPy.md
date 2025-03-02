---
title: "DSPy"
---

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
