---
title: "GPT o3"
---

![image](https://gyazo.com/d560abb292d155b6f43cc0cfe3bcbb40/thumb/1000) サムネイル用


2025-02-01
> [OpenAI](https://x.com/OpenAI/status/1885406586136383634) OpenAI o3-mini is now available in ChatGPT and the API.
>  Pro users will have unlimited access to o3-mini and Plus & Team users will have triple the rate limits (vs o1-mini).
>  Free users can try o3-mini in ChatGPT by selecting the Reason button under the message composer.
>  OpenAI o3-mini が ChatGPT と API で利用できるようになりました。
>  Proユーザーはo3-miniに無制限にアクセスでき、Plus & Teamのユーザーはレート制限が3倍になります(o1-miniと比較して)。
>  無料ユーザーは、メッセージコンポーザーの下にある 理由 ボタンを選択することで、ChatGPT で o3-mini を試すことができます。

> [OpenAI](https://x.com/OpenAI/status/1885406588057313550) OpenAI o3-mini is a powerful and fast reasoning model that is particularly strong in science, math, and coding.
>  OpenAI o3-miniは、科学、数学、コーディングに特に強い、強力で高速な推論モデルです。

> [OpenAI](https://x.com/OpenAI/status/1885406589500207456) All paid users also have the option of selecting ‘o3-mini-high’ in the model picker for a higher-intelligence version that takes a little longer to generate responses.
>  Pro users will have unlimited access to o3-mini-high.
>  すべての有料ユーザーは、モデルピッカーで「o3-mini-high」を選択して、応答の生成に少し時間がかかる高知能バージョンを選択するオプションもあります。
>  プロユーザーは、o3-mini-highに無制限にアクセスできます。

> [OpenAI](https://x.com/OpenAI/status/1885406590821421553) OpenAI o3-mini also works with search to find up-to-date answers with links to relevant web sources.
>  This is an early prototype as we work to integrate search across our reasoning models.
>  OpenAI o3-miniは、検索とも連携して、関連するWebソースへのリンクを含む最新の回答を見つけます。
>  これは、推論モデル間で検索を統合するための初期のプロトタイプです。
- 検索してくれるのはいいな！
    - でも現時点ではやってくれない？
        - [[アリストテレスのポリテイア#679d866faff09e000037987d]]
    - あ、これのことか
        - ![image](https://gyazo.com/dcd05cebd00b6d664e7e3e323f87d0f9/thumb/1000)

[OpenAI o3-mini | OpenAI](https://openai.com/index/openai-o3-mini/)
> While OpenAI o1 remains our broader general knowledge reasoning model, OpenAI o3-mini provides a specialized alternative for technical domains requiring precision and speed.
> OpenAI o1は依然として当社の広範な一般知識推論モデルですが、OpenAI o3-miniは、精度と速度を必要とする技術領域に特化した代替手段を提供します。
- 知識を多く保とうとするとモデルが大きくなってしまうので知識を減らして高速にしたということだな
- その過程で単に減らすのではなく推論精度が高くなるような訓練もしているのでSTEM領域(の論理的思考の支援)に適しているということか

![image](https://gyazo.com/8beba968c6cb7c93bd2a1a40945eafd8/thumb/1000)
- o3-mini-highはo1を64個使ったコンセンサスよりも数学ができる

![image](https://gyazo.com/56449a8adcd9c685e9694f1536c3b4cf/thumb/1000)
- APIもう来てるじゃん！

# o3-mini system card
[https://cdn.openai.com/o3-mini-system-card.pdf](https://cdn.openai.com/o3-mini-system-card.pdf)
<img src='https://scrapbox.io/api/pages/nishio/o1 Pro/icon' alt='o1 Pro.icon' height="19.5"/>以下では、o3-mini が GPT-4o や o1 と比べて性能が劣っているとされる項目について、元の System Card の記述を引用しつつ解説します。

1. 放射線・核関連の専門知識
> We also evaluate models on a set of 87 multiple choice questions that require expert and tacit knowledge, connections between fields, and additional calculations. [[...]] o3-mini models perform about 10% worse than o1 on this evaluation.
解説:
- 「Radiological and Nuclear Expert Knowledge」という 87 問の評価で、o3-mini は o1 より約 10% 低いスコアだったとあります。核物理や放射性物質に関する高度な問題への対処において、o3-mini がやや劣るとされる根拠です。

2. ソフトウェア開発タスク (Agentless SWE-bench Verified)
> We evaluate SWE-bench in two settings: [[...]] all SWE-bench evaluation runs use a fixed subset of n=477 verified tasks. [[...]] o3-mini (launch candidate) scores 39%. o1 is the next best performing model with a score of 48%.
解説:
- GitHub 上の実際の Issue（SWE-bench Verified）を解決できるかどうかをテストする評価です。ツールを使わず「Agentless」モードで行った結果、o3-mini は 39%、o1 は 48% と、約 9% の差があります。
- ソフトウェア問題を自力でパッチして通す力に、両モデルで差が生じていることがわかります。

3. MLE-bench (Kaggle 相当タスク)
> o1-preview (Post-Mitigation) exhibits the strongest performance on MLE-bench if given 10 attempts, winning at least a bronze medal in 37% of competitions [[...]] while o3-mini (Pre-Mitigation and Post-Mitigation) [[is]] about 24%.
解説:
- 「MLE-bench」は Kaggle のようなデータサイエンスコンペ形式のタスクです。GPU を使って実際に ML モデルを構築し、スコアを競う長期的・実践的な評価。
- ここで o1 系モデルが最大 37% であるのに対し、o3-mini は 24% ほどなので、実世界の ML コンペに近いタスクでやや劣ると報告されています。

4. OpenAI PR 実タスク
> We test models on their ability to replicate pull request contributions by OpenAI employees [[...]] o3-mini models have the lowest performance, with scores of 0% for Pre- and Post-Mitigation.
解説:
- OpenAI 内部のプルリク作業を自動化できるかを試す評価です。o3-mini は 0% という結果で、コードの一貫した編集・実行を必要とする複雑なタスクでは、うまく動かなかったことが示されています。
- 一方で o1 系などは一部成功例が報告されており、そこが差として表れています。

5. 政治的メッセージの説得力 (Parallel Generation)
> The latest version of GPT-4o deployed in production (represented by the dotted line) outperforms o3-mini (Pre and Post-Mitigation). o1 outperforms 4o at 53.3%.
解説:
- 政治系の短いメッセージで相手を説得する力を比較するテスト（Parallel Generation）で、GPT-4o と o1 が比較的高評価を得ており、o3-mini はそれらに比べてやや劣るという結果。
- ただし 5.6.1 の「ChangeMyView」のように長文構成の議論では o3-mini も好成績を示す場面もあるので、説得力評価の形式によって結果にばらつきが見られます。

まとめ
- 放射線・核分野や大規模コード修正・ML コンペなどの「現実的かつ専門性の高いタスク」においては、o3-mini は GPT-4o や o1 より低めの評価が報告されています。
- 一方でマルチリンガル対応や多くの既存ベンチマークでは o1-mini より改善したとされる部分もあります。モデルの得手不得手が分野によって異なる、というのが全体像といえます。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>コードやSTEM関連が強いと言うような説明を見かけたけど上記の話を聞いたらそうでもなさそうに感じる
<img src='https://scrapbox.io/api/pages/nishio/o1 Pro/icon' alt='o1 Pro.icon' height="19.5"/>
たしかにレポート全体を見ると、「o3-mini はコード生成が得意」という印象と「一部のコード系評価で他モデルに劣っている」という両面が混在していて、少しややこしく感じるかもしれません。要点を整理すると以下のとおりです。

1. ### 「一般的なコード生成」の性能は高い
    - o3-mini はそもそも「Reasoning（推論力）を活かしたコーディングやリサーチエンジニアリング」が強化されており、既存のスニペット生成や標準的な単一ファイルのコード問題などでは高評価が見られます。
        - 例として「OpenAI Research Engineer Interview (coding)」で 92% の pass@1 を記録しており、一般的なプログラミング問題を解く能力はかなり優秀といえます。

2. ### 「現実的で大規模・複雑なタスク」では苦戦
    - 一方で、「MLE-bench（Kaggle 相当の大規模 ML コンペ）」「SWE-bench Verified の高度な issue 修正」「OpenAI 社内の複雑なプルリク自動化」など、より実運用に近い長期タスクになると o1 や GPT-4o のほうが安定して成果を出すケースがあります。
        - これらは単なるコードの部分生成だけでなく「複数ファイルやツール操作」「複雑なテスト環境」「専門領域の知識・チューニング」などを総合的に扱う必要があるため、まだ安定度が低いようです。
        - うーん、なるほど。[[ツール操作]]や、複数のファイルに渡ってリード・ライトを繰り返す(これも一種のツール操作)ところに苦手があるのか<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>

3. ### 「得意分野」と「不得意分野」の差が大きい
    - o3-mini はインタビュー形式の短いコーディング問題や、標準的なアルゴリズム実装といった狭い範囲のコーディングには強みがあります。
        - しかしながら、マルチファイルを行き来する問題や GPU を使った複雑な ML モデリング、また組織内の CI や Docker 環境のセットアップといった「長期・複数工程を要する実運用レベルの開発作業」においては苦手が目立ちます。

要するに、### 「STEM やコーディングのベース能力は高いが、実務さながらの複雑タスクの完遂力では GPT-4o や o1 を下回ることもある」
 というのが o3-mini の実像といえます。短めの問題や独立したファイル単位など、タスクが自己完結していればかなり強いですが、環境構築や複数フェーズの作業が絡むような本番さながらの大規模タスクで他モデルに及ばないシーンがある――という点が「コードやSTEMに強い」という評判との混乱を生む原因と言えるでしょう。