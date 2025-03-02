---
title: "ChatGPTに出しているプログラミング指示"
---

うまくいくことがほとんどなので記録してなかったが、うまくいかない人に「どんなことやってるの」と聞かれた時に共有するための事例メモ
- 特に何も書いてないものは特に問題なく動いたと言うこと


---
[[git update-index --skip-worktree]]

---
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
下記のcodeで記録されたデータがある
conversationごとに時系列で「クラスタ数」を表示したい
Pythonで書いて
<code>

(備考) "下記のcode"がNode.jsだったので生成コードも同様になった、Pythonが良かったのでプロンプト編集した。"下記のcode"はAPIを叩いて保存するだけなので、JSONデータのスキーマが不明であり、そこは仮のコードになった

---
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
クラスタ数のアクセスを見つけて
<json>

<img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>
このJSON構造を見る限り、クラスタに関連する情報はgroup-clustersキーに保存されています。このキーは、クラスタのIDとその中心座標、またクラスタに含まれるメンバーのリストを持つオブジェクトの配列です。クラスタ数は、このgroup-clustersの要素数を数えることで取得できます。
<code>

---
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
このコードの後に「Conversation IDごとに、最もクラスタ数が多くて、その中で最も新しいデータ」をprintするコードをつけて。追加部分だけの表示で良い

---
JavaScriptとPythonのDateオブジェクトの文字列化の違いによるバグを直させる
元のコード
py

```
# 該当するJSONファイルを開く
filename = f"{conversation_id}-{max_cluster_record[0].strftime('%Y-%m-%dT%H-%M-%S.%fZ').replace(':', '-')}.json"
```


<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
`strftime('%Y-%m-%dT%H-%M-%S.%fZ')`
ここのZは3桁

<img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>
以下のように変更して、ミリ秒形式で表示できるようにします。
py

```
# ファイル名のタイムスタンプを3桁のミリ秒にフォーマット
filename = f"{conversation_id}-{max_cluster_record[0].strftime('%Y-%m-%dT%H-%M-%S')}.{max_cluster_record[0].strftime('%f')[:3]}Z.json"
```



---
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
下記の資料をもとにIDとhuman readableなtitleの対応dictを作って
<document>


---
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>matrixはPandasのDataFrameであり592人のデータがある。これをUMAPで可視化したい。UserのIDは他の属性情報と紐づけられるので後で使いたい。実装して

---
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>dataというDataFrameにPARTYとして整数で政党データがある。これの政党名とのmapは下記、これをScatterの点として表現したい

(補足)この指示では「dataから有効なものだけ抜き出したのがmatrixであり対応づけなければならない」ということはわからなかったようで、別途指示し直す必要があった

---
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>matplotlibのscatterに関して、虫眼鏡アイコンでデータを絞り込んで再描画できるじゃないですか。その絞り込んだ範囲がなんであるのかイベントリスナ的なものを追加して表示することはできます？
<img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>[https://chatgpt.com/share/6723a783-b0b4-8011-8c54-52ef24defc80](https://chatgpt.com/share/6723a783-b0b4-8011-8c54-52ef24defc80)

便利~~
---
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>下記のようにscatterで点を出さずにテキストで表現している、このときlegendにそのテキストが例として出ない。legendにテキストを出すか、それが難しいときは色を示すpatchを出したい。
<code>

----
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>matplotlibですでにshowしたscatterの`Selected range: x=[-14.85, -9.30], y=[6.60, 10.22]`だけ拡大して再掲したい
<img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>(scatterをやり直すコード)
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>scatterをやり直さない方法はない？

(あったけどそもそもscatterがテキストで表示してたので再描画は必要だった)

---
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>賛成+1, 反対-1, 欠損0の100次元ベクトルを5000個つくれ。なお+1と-1の確率は同等で、欠損でない値が3件以下になる確率を20%程度とする

(数式の微修正が必要だった)
---
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>dataの中の同じ値のベクトルの個数を集計して多い順に10個だすコードを書いて

---
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>下記のようなjsonlを受け取ってcomment-id,comment-bodyのCSVを作るPythonコードを書いて

---
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>日本の政党をグラフ表示するときに適したカラーのPythonのdictをつくって
