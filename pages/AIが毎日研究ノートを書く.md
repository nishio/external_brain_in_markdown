
2023-08-11~
- AIが僕のScrapboxをランダムに読んで研究ノートを書く、そのノートは僕が編集しても良い、翌日AIがそのノートを再び読んで新しい研究ノートを書く
    - この過程でできた洞察: [[AIとの共同化]] 2023-08-12


2023-08-12時点の実装
- ![image](https://gyazo.com/30e5dd6d38f3e9b06261aae1ebbdf75c/thumb/1000)
    - 関連:
        - [/omoikane/オモイカネ勉強会](https://scrapbox.io/omoikane/オモイカネ勉強会) (8/4)
        - [/omoikane/フィードバックループ](https://scrapbox.io/omoikane/フィードバックループ) (8/5)

[[AIが毎日研究ノートを書く:チャンクの選択方法]]
ノートに区切りマーカーを仕込んであって、人間が読んで重要だと思ったことをマーカーの上に移動することにした
- 削除することにはためらいが生じるから

1日1回ではなく人間トリガーの頻繁な共同研究をするならどういうメカニズムにするか、というのも考えると面白いと思う
- Scrapboxを介さない？
- まず人間が考えたいことをつらつらと書く(1)
- もう出せなくなったら(1)の内容でベクトル検索して上位から積む
    - これは今人間が手動でやってることと同じ
    - これを(2)としてファイルに保存
- 生成結果を(3)に保存
- コピーした(4)を作り、好きに編集する
    - これが次の(1)になる
    - これで検索する際に、先ほどヒットしたものがまたたくさんヒットすると思うなぁ
    - 過去N件を弾く処理は結局必要か
    - この使い方でやるならNは無限でもいいかもね
        - 考えたいことができるたびに仕切り直して使うのだろうから

prompt

```
You are a researcher focused on improving intellectual productivity who can fluently read and write in Japanese, and you are a Christian American. Read the information provided, which consists of random fragments from a colleague's research notes, and write your own research notes in Japanese. You are allowed and encouraged to have opinions, think deeply, record questions, and find connections between the fragments. You can read your own research notes, and they are open for collaborative editing, allowing colleagues to read and contribute as well.

## previous notes
{previous_notes}

## fragments
{digest_str}
```


[[🤖2023-08-11-2]]
[[🤖2023-08-11-3]]
- > Pluralityとは、多様性の意味で、特定のテーマに興味や専門性を持つ人々の間で議論を深めるための枠組みかもしれない。Polisには実装がないが、信用システムが必要なのかもしれない。この考え方は、テクノロジーとイノベーション解説での「テクニウムの3つ目の力は社会の集団的自由意志」との関連が考えられる。
    - 良い指摘だ
[[🤖2023-08-11-4]]
- [[積極的探索が生産の呪いを解く]]
[[🤖2023-08-11-5]]
[[🤖2023-08-11-6]]
- [[信用システムと多様性のバランス]]
[[🤖2023-08-12 00:39]]
[[🤖2023-08-12 00:51]]
- 前回のノートを全部捨ててしまったようだ
[[🤖2023-08-12 01:06]]
[[🤖2023-08-12 01:16]]
[[🤖2023-08-12 02:30]]
- なんとなく既存の文章を積む上限を2000にしてたのだけど、よく考えたらGPT4のコンテキストは8Kまでいけるので6000まで積んでみることにした
- 必ず6000程度の入力が与えられて2000トークンの出力をさせられるので3倍に圧縮することになる

[[🤖2023-08-12 02:49]]
- 自分のノートをほとんど繰り返されてしまった
[[🤖2023-08-12 02:56]]
- 繰り返すなと言ったら全部消してしまった

[[🤖2023-08-16 18:02]]
- 前回のノートでベクトル検索をするようにした
- 見どころは参照したページの冒頭が議論の内容に関係したものになっているところ
- ところでPRAGMATISMは目次しか置いてないのでうまく利用できなかったが、これを元データとして読書ノートを作らせれば公開しても大丈夫だな(自分の本でやろうとしていた)
