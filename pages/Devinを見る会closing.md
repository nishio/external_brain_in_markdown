---
title: "Devinを見る会closing"
---

[[Devinを見る会]]

結局いくらかかったのか
- ![image](https://gyazo.com/b6b57b3997f4da39fa5bf587a9e53d8b/thumb/1000)
- 毎月のmininumの250ACUを使い切った後は100ACUずつ追加していた。100ACUで200USDで、1USDは150JPYをちょっと超えたくらい(今日時点で157円)なので1回3万円ちょい、総額27万円という感じ。

[[Devinで4万溶かす方法]]

2025-01-25
2. ### Devin関連の「非公開化＆体制再構築」タスク
    - T8567: Devinの非公開化
    - T8568: 個人Slackへの接続移行
    - T8569: WebUIメンバーの整理
    - T8570: リポジトリをすべてprivateにする
    - T8571: クロージング記事の作成
        - これらは相互依存が強く、まとめて「Devinを個人用途に特化させる」フェーズとして進める必要がある。クロージング記事を公開するタイミングや、後方タスク（T8572, T8573など）も考慮すると、早めに着手して段階的に完了していくのが望ましい。

### T8568
: 個人Slackへの接続移行
![image](https://gyazo.com/09fd23abfe8c847e3cce0c6db6af68a2/thumb/1000)
- ✅

### T8569
: WebUIメンバーの整理✅

![image](https://gyazo.com/f3caa8685411e8e052a9434792621393/thumb/1000)

![image](https://gyazo.com/2a876e8019f2696bdb9df8815388b150/thumb/1000)
これOFFにしよ

### T8570
: リポジトリをすべてprivateにする
- これsnapshotをbaseに戻す方法がわからないな
- 単純に削除するか
- 削除してスナップショット保存をしたらonbodingの画面になった
    - ![image](https://gyazo.com/aac290c8e5cac82eac97bfc7535b44c7/thumb/1000)

知識を整理する
- ![image](https://gyazo.com/6ee8596012eed9f5d1fd352c20390126/thumb/1000)
- ウケる。常にやれw

知識は(Pin to Repositoryされてない限り)ある種のグローバル変数のようなものでチームメンバー全体に影響を及ぼすわけだが、影響範囲とか考えずにapproveしちゃう人は多くの組織で発生するだろうなぁ
- 誰かが適当に承認した知識のせいで振る舞いが変わって変なことをするようになるとか、デバッグ困難だよなぁ

### T8570
: リポジトリをすべてprivateにする
- これは適切ではない気がしてきたのでclosedにする
    - いまpublis repoの中でprivate repoのdataをcloneしているが、private repoの中でpublic repoからcloneするとか、むしろpip installしてしまうのが良いのでは、という話もある

