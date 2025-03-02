
2022-01-17 できた
- スマホから当日のワークアウトを、ワークアウトの名前を手動で入力したり日付を入力したりすることなく入力できる
- 各ワークアウトには任意の長さの自由記述ができる

---

- レコードからタイトルフィールドを削除することはできない？
    - できなさげ
    - [https://www.reddit.com/r/Notion/comments/hadrpu/a_table_without_a_title_column/](https://www.reddit.com/r/Notion/comments/hadrpu/a_table_without_a_title_column/)
- カレンダービューでタイトルフィールドを非表示にすることはできない？

うーん
つまりすべての情報の基底クラスが「ページ」であり「タイトル」フィールドを持ってるというわけだ
- 微妙〜

![image](https://gyazo.com/c36d413a63979421aa06ac1d1ba60454/thumb/1000)
![image](https://gyazo.com/c81a225dc440dc2c4f22784d8a7855c9/thumb/1000)
- 微妙〜

![image](https://gyazo.com/6ca9d43b06c88dbd1db389670add20b0/thumb/1000)

うーむ
例えば筋トレ内容ごとに別のページにし、内容を1行でタイトルに書けばいい？でもそれは「個別のレコードにするのがめんどくさい」って言ってやらなくなりそう

いっそNotionではなくkintoneが良いのでは
![image](https://gyazo.com/9b19e16615bf303106ab4990914912b8/thumb/1000)
![image](https://gyazo.com/4ae4f34f46eb6a681980bd7cb0597499/thumb/1000)

マルチセレクトをカレンダービューの表示対象にできないか…
- タイトルを指定していないのでレコードIDが表示されている
- JSカスタマイズで見た目を変えることは可能だが…



これ「カレンダーに表示できる」程度のメリットのためにゴチャゴチャNotionで作り込んだら、筋トレメモを書くのがめんどくさくて筋トレしなくなりそうだ

Scrapboxの絞り込みが貧弱なせいで「Scrapboxでやると既存のネットワークを破壊したり遅くなったりするのでは」と不安になってNotionでやろうとしたが、本当に必要なのはScrapboxで別のプロジェクトとしてやることかもしれない。

![image](https://gyazo.com/4dfa675f4f390ac57d56a9d373ab0170/thumb/1000)
![image](https://gyazo.com/15fd63427bd1412edd70390ebee25c4f/thumb/1000)
これでいい気がするな…
- たしかにカレンダービューではないのだけど「カレンダービューであることが本当に重要な要件ですか？」というやつ

本当に重要な要件はなんなのか
- 筋トレをした時にストレスなくメモできること
- 振り返りやすい(とは何か)
- 手軽にメモを取れる必要がある
    - 公園でメモをとることがあるのでスマホで。PCを要求しない
    - メモを取ろうと思った時にする作業が少ない必要がある

妻から動画が送られてきた
[https://www.youtube.com/watch?v=ZQ-uUtHHyzc&feature=youtu.be](https://www.youtube.com/watch?v=ZQ-uUtHHyzc&feature=youtu.be)
あー、なるほど。テンプレートボタンは試して「いや、テキストが追加されてもな…」と思ってたんだが、そこにレコードを突っ込むことができるのか。

作った
- ![image](https://gyazo.com/fcaf1de8e87f055315ce14a0aea97cf6/thumb/1000)

スマホではカレンダービューに対するドラッグドロップができない
カレンダービューへのドラッグ以外の方法で日時を入れるには
- カレンダービューの表示に使う日時を作成日時にする案
    - 後から編集はできないので筋トレした日に確実にレコードを作成する義務が生じるが、それをやるなら問題はない
    - いやダメだ、昨日以前の筋トレのデータを入れることが出来なくなる
- 公園では日付の入ってないレコードを追加し、帰ってきてからカレンダービューの適切な場所に入れる
- Q:Dateに「@today」すれば生成時に今日の日付が入るのでは？
    - A:Date型はテキストではないのでinvalidになる

「レコードのタイトルが特定の文字列を含む」という絞り込みができるので、各絞り込みを生成しておけば過去の振り返りが簡単
![image](https://gyazo.com/7cdb505e6b5bbfcd06781fe599edb415/thumb/1000)
できそうな気はして来たがめんどくさい気持ちが高まってきた

追記
- 妻から「Linked Databaseでできるのでは」という提案
- Linked Databaseを使って「今日の」「タイトルにバーハングを含む」というデータベースを作っておけば、追加ボタンを押すだけでそれらの値が自動挿入されたレコードができる
- 追加に対してドラッグなどが必要ないのでスマホでも問題なく動くことを確認した

というわけで改めてゼロから作ってみよう
まず空のページを作る
![image](https://gyazo.com/6df60c4b352049bb96661a7eaab840db/thumb/1000)
そしてデータベースを作る
![image](https://gyazo.com/0773c2091f5c7f687c7dbd1749689937/thumb/1000)

Linked Databaseをつくる
![image](https://gyazo.com/541fca1871f77454c18543e2faa9e48e/thumb/1000)
FilterでToday
![image](https://gyazo.com/63313783ea4de2f140fbcadc5a278789/thumb/1000)
DuplicateしてFilterを追加
![image](https://gyazo.com/b50a33497d7ce50f50ddb5d6cd4466ab/thumb/1000)
全種類のワークアウトに対応するLinked Databaseを使って曜日に割り振る
できた
![image](https://gyazo.com/cc7c4810d7891f1e09cf62435ce7044b/thumb/1000)
データを入れるところがスムーズになれば履歴を見るところは後からでも良い

2022-01-17
筋トレは週に2回なのでデータがあんまり入っていかない、ストレッチも一緒に記録しようかな

[https://twitter.com/mizukih__/status/1481944275860750340?s=21](https://twitter.com/mizukih__/status/1481944275860750340?s=21)
前後のレコードがすぐ見れるから「前回スクワットした時何回やったっけな」もすぐ見れるね、よい

![image](https://gyazo.com/bd68ebac742b1596332a749fad4e46fd/thumb/1000)
- 最初に入れるタイトルを変えるのに関してはLinked Databaseを個別に作らなくてもテンプレートで良い
    - テンプレートで日付の初期値を「今日」にする方法ないのかな…
- あれ？ダメだ
    - テンプレートではタイトルに値が入ってるのにレコード作成すると消えるぞ
    - 2年前から言われてる
        - [https://www.reddit.com/r/Notion/comments/e5ih9g/automatically_insert_a_title_for_pages_opened/](https://www.reddit.com/r/Notion/comments/e5ih9g/automatically_insert_a_title_for_pages_opened/)

NotionとScrapboxのかなり本質的な違い
- Notionはレコードのタイトルが同じ文字列でも良い
- Scrapboxはページのタイトルが同じ文字列だとまとめようとしてくる
Wikiとしてはまとめるのが自然だし、データベースだとまとめないのが自然


2022-01-18
- ![image](https://gyazo.com/6e759c128710cf4cdc098710ac3ce971/thumb/1000)![image](https://gyazo.com/ad49890520afee989d5433ea7248a4fe/thumb/1000)
- スマホからの入力は支障ないが、表示で肝心の運動回数が隠れてしまっている
    - スマホの横幅が狭いから
- 日付のフォーマット変更で年を削ることはできない
- 日付自体の表示欄を右に移動した
    - ![image](https://gyazo.com/9dce20c5713a2257e5ec3fd511867d2f/thumb/1000)

振り返り用のギャラリービュー
- ![image](https://gyazo.com/76e4c8d7ebcd0cdab366285df2d6fa26/thumb/1000)
