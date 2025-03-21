---
title: "ベクトル検索とRAGの肌感の違い"
---

from [[日記2023-09-02]]
[[ベクトル検索]]と[[RAG]]の[[肌感]]の違い

最近[[AIによる赤リンクの延伸]]が便利なので使いまくっているのだけど、[[西尾のベクトル検索]]を使いまくっていた時とは肌感に違いがあって、それはなんなのだろうと考えていた
- [[検索結果は編集をアフォードしない]]
- Scrapboxに書かれたものは[[編集をアフォード]]する
    - それはScrapboxが共同編集のツールだから
    - RAGかどうかではない
        - チャットの相手側の発言も編集をアフォードしない
- [[書くのではなく削ることによる考えのアウトプット]]のことを考えるとAI出力は編集をアフォードする必要がある

RAG: [[RETRIEVAL-AUGMENTED GENERATION]]

8/29
> [kazunori_279](https://twitter.com/kazunori_279/status/1696336555215053072) やっぱファインチューンとかRAGとかごにょごにょするより、単純にembでベクトル検索して結果を表示するだけで良くね？って思った。
> [LLMのファインチューニング で 何ができて 何ができないのか｜npaka](https://note.com/npaka/n/nec63c01f7ee8)
- > [nishio](https://twitter.com/nishio/status/1696396921903190238) 僕もながらく「ベクトル検索だけでいいだろ」派だったのだけど、単なる質問回答ではなく知的生産のアシスタントとして使う場合はRAGの方がいいと感じる。生成部分が「[[目的に合わせて検索結果を要約する]]こと」として機能するので。なおこれはクエリとは別に目的が与えられてることが前提。
- > [kazunori_279](https://twitter.com/kazunori_279/status/1696424311870148981) たしかに、ユーザーとの対話とアシストがメインのサービスならばRAGは役立ちますね。

[[説明のある検索]]

__BELOW_IS_AI_GENERATED__
# ベクトル検索とRAGの肌感の違い
 2023-10-05 16:53 <img src='https://scrapbox.io/api/pages/nishio/omni/icon' alt='omni.icon' height="19.5"/>
## ダイジェスト
「ベクトル検索」と「RAG」の使用感の違いについて考察。Scrapboxは共同編集ツールであり、編集をアフォードする。AI出力も編集をアフォードする必要があると主張。また、ベクトル検索とRAGの違いについてTwitter上での議論を紹介。

## フラグメントとの関連性
「next勉強会」の断片は、ベクトル検索の利点と欠点について述べており、ノートの「ベクトル検索」と「RAG」の使用感の違いと関連している。「横断ベクトル検索実験メモ2023-09-20」の断片は、ベクトル検索の実験について述べており、ノートのベクトル検索の使用感と関連している。「RAG」の断片は、RAGの概念を説明しており、ノートのRAGの使用感と関連している。

## 深い思考
ベクトル検索とRAGの使用感の違いは、それぞれが提供する「編集のアフォード」の違いによるものかもしれない。ベクトル検索は結果をそのまま表示するが、RAGは検索結果を要約し、目的に合わせて表示する。これにより、RAGはユーザーが情報を編集しやすい環境を提供する。

## 考えの要約
ベクトル検索とRAGの使用感の違いは、それぞれが提供する「編集のアフォード」の違いによる。

## タイトル
「ベクトル検索とRAGの使用感の違い：編集のアフォードの視点から」

### extra info
titles: `["next勉強会", "横断ベクトル検索実験メモ2023-09-20", "RAG", "結局必要なのは検索の精度向上", "pVectorSearch2023-04-29~05-31", "AIとの協働作業の実態とS字カーブ"]`
[[LLMによる知的生産性向上勉強会]]
[[横断ベクトル検索実験メモ2023-09-20]]
[[RAG]]
[[結局必要なのは検索の精度向上]]
[[pVectorSearch2023-04-29~05-31]]
[[AIとの協働作業の実態とS字カーブ]]
fragments

```
### next勉強会
	ベクトル検索、フワッとヒットするので自然言語の会話の曖昧検索には良いが「営業で訪問した相手先企業名」とか「製品型番」とかだと「見た目のよく似た違うもの」もヒットするのでユーザの認知負荷が高い


以下は、入力された情報を要約したものです：[gpt.icon]
	7/29: AIがScrapboxに書き込み、Scrapboxエージェントの概念を紹介。
	8月の初めから中旬: オモイカネ勉強会、AIとの連携に関する議論、AIによる研究ノートの執筆、ベクトル検索の進化、及びAI生成ページの取り扱いに関するトピック。
	8月の中旬から終わり: マルチヘッド、ページメモリ、ユーザーの認知負荷を考慮した更新と検索に関するトピック。
	9月の初め: AIとユーザーとの相互作用、ノートの管理、及び異なるコンテンツ間の関連性を探求。
	9月の中旬: マルチヘッドの思考、エンジニアの知的生産術、AIとの連携に関するさまざまなトピック。
	9月の後半: LLMと他のモデルの比較、人間の概念に関する議論、Scrapboxの最適な使用方法、及び非公開ツールのフィードバック。
全体として、この期間はScrapboxとAIとの連携、特にベクトル検索やマルチヘッドの概念、AIの思考とユーザーとの相互作用に重点を置いているようです。


### 横断ベクトル検索実験メモ2023-09-20
横断ベクトル検索実験メモ2023-09-20
このScrapbox上で今まで公開して実行してきた[AIによる赤リンクの延伸]の、検索対象データを増やす実験を行った
	検索対象には他人のScrapboxのデータ、書籍や論文が含まれる
		関連
		　[蔵書横断ベクトル検索]
  		[書籍をScrapboxに入れる話]
  		[個別のループと集約したループ]
	生成結果をそのままレビューなしに公開することには何か問題が発生する可能性があるので、出力先は非公開のプライベートプロジェクトにした
　	その後のアップデートで検索にヒットした部分をそのままScrapboxに出力するように変えたのではっきりと公開不可能になった

[https://gyazo.com/bb1a0bd6cb151fa1b6ffa2d7c498744c]
　こんな感じで作った赤リンクの先にAIによって自動的にページが生成される

実装
　ローカルのpickleからロード
　　10万件のレコードを読むのに5秒程度
　ローカルでベクトル検索を行うのに7秒程度
　Webアプリのレスポンスと考えると遅いが、最近の「思いついたキーワードやページを投げておいて別の作業をし、しばらく経ってから見る」というスタイルでは問題にならない
　　クエリを投げてから僕が結果を確認しに来るまで(計測はしてないけど)10〜25分くらいある


### RAG
RAG
[生成AI]に[検索を組み合わせる]

[Retrieval-Augmented Generation]
[Retrieval-Augmented Text Generation]



### 結局必要なのは検索の精度向上

>[nishio https://twitter.com/nishio/status/1704379950743339227] 生成AIをちゃんと生成に使うと有効なんだけど、そもそも顧客って生成がしたいんだっけ？と考えると、大部分の顧客のニーズは「読むのがしんどいたくさんのものの中から重要なところを見つけて欲しい」で、最終的に生成するとしても手前に「生成の材料を見つけて欲しい」があるから結局検索が必要的な話

>[nishio https://twitter.com/nishio/status/1704380927970009522] 話が若干違ってて「従来技術の方がいい」とは全く思わない。すでに自分が従来の検索も自分で作ったベクトル検索もほとんど使わずに[RAG]ばかり使うようになってるから。なのだけど、それの有用さを上げていくとき競争のドメインはスパースな検索とデンスな検索を組み合わせたりリランクしたりになる感



### pVectorSearch2023-04-29~05-31
　　　これが面白そう
　　　　例えば「誤った二分法」とリクエストに積むとレスポンスに`https://gyazo.com/80d45ec33ca8cbb138108d71ad7eec02`が返ってくる
　　　　	[[誤った二分法.icon]]
　　　　[盲点カード]をランダムに引くのではなく今書いている文章でのベクトルサーチで引くことができる
　　　　これはScrapboxの「ページ」という形で「画像」と「文章」のペアを溜め込んでいるからこそできること
　　　　[画像と文章のペアに価値がある]

2023-05-04
 [自分のScrapboxをベクトル検索して2hopリンクをたどる]
		ベクトル検索して画像を見ている事例

2023-05-11
	[質問を収集して改善する]のは面白いかもな

2023/5/16
　音声で喋ってる時に音声認識して、自動的にそれをクエリにしてこのScrapboxを検索し、マッチしたものを表示するシステム
　喋りに対する「関連ページ」
　　最初「画像だけ検索」って思ってたけど、画像のないページもScrapboxの関連ページフォーマットで表示すれば良いやと思った

2023/5/31
　[個人の知識ネットワークの相互作用]
　[他人のScrapboxもベクトル検索したい]
　この辺りのことを踏まえて「自分以外のものも含めてベクトル検索」できると良いのかも
　というのは「西尾泰和のScrapbox」をベクトル検索する機能は僕に取っては、僕以外の人がその機能に対して感じるものと異なった見え方になるので、何がどうなるといいのかまったく共感できないからだ


### AIとの協働作業の実態とS字カーブ
		「キリのいいところまで書いてAIに渡す」という体験の方が勝ってる
	9/1には「[ベクトル検索とRAGの肌感の違い]」を書いてる
		「[編集をアフォード]する」
	9/9には「[文脈付きで推薦]」と解釈している

__BELOW_IS_AI_GENERATED__
[*** AIとの協働作業の実態とS字カーブ] 2023-09-18 00:24 [omni.icon]
[** ダイジェスト]
AIとの協働作業は、思考の停滞期を感知し、AIに内容を投げて別の作業に移行する。人間の思考はS字カーブを描き、停滞期にはAIが役立つ。AIとの協働作業は、作業Aから作業Bへの移行をスムーズに行う。また、AIとの協働作業は、思考の停滞期を感知し、AIに内容を投げて別の作業に移行することで、思考の停滞期を避けることができる。

[** フラグメントとの関連性]
「AIと人間の知的な共同作業」のフラグメントは、AIと人間の協働作業の具体的な例を示しており、ノートと直接関連している。具体的には、AIと人間がチームメンバーとなり、新しいチームワークの形を作り出すという点が、ノートで述べられているAIとの協働作業と一致している。

[** 深い思考]
AIと人間の協働作業は、思考の停滞期を感知し、AIに内容を投げて別の作業に移行することで、思考の停滞期を避けることができる。これは、人間の思考がS字カーブを描くという特性を利用したものであり、AIと人間の協働作業の有効性を示している。


```

generated: 2023-10-05 16:53