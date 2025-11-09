---
title: "pConceptMap2025-09-09"
---

[[pConceptMap]]
- prev [[pConceptMap2025-09-08]]

scriptを雑にplurality repoにおいて実験してたけど、リリースを考えると独立したrepoでVercelとかにするのがよいのでお片付け

現状はHTMLファイルの置換でプロトタイプが作られてたけど、React的なもので作ってUIの改善サイクルを効率良くしたい
最終的には静的HTMLを書き出してリリースしたい

git worktreeをやってみる

prompts.pyの改善
- "tier": "core"|"supplementary"|"advanced" これは削除する
    - 将来的にmax_conceptsを変えて抽出することでtierをつくる
- Allowed relation types (choose one): {relation_types} この限定も削除する
    - 関係は対象を含む短文で表現する

![image](https://gyazo.com/4aaf806256e93599ddd0aab216d69c4f/thumb/1000)

並行移動してからノードをクリックした時に並行移動がリセットされるバグ

relationは今文章だが、これをrelation_descriptionというフィールド名にし、relationには可能なら1単語、多くても3単語の短い表現を入れるようにしたい。これはグラフ描画時にエッジのラベルとして表示するためである。
- ![image](https://gyazo.com/5a35e5824f617395efe626282b8f4a61/thumb/1000)


引用文に`**`が含まれるとビューとしてはイマイチだが、出現箇所を見るのには残した方がいいのか？
- WebUIの表示部分を単にMarkdownコンポーネントにする手もあるか

リレーションラベルをクリックしたらそのリレーションの情報(引用など)が、いまノードの情報が出ているのの下に出るといいと思う
- ![image](https://gyazo.com/4db9e134e44528ef00c442379d158796/thumb/1000)

![image](https://gyazo.com/6ebed93497e9f913cbef78a985111263/thumb/1000)![image](https://gyazo.com/d781b407bbf1e940c69e757f2560c372/thumb/1000)


カードで詳細表示している概念や関係は左のグラフでハイライトされるようにしよう

![image](https://gyazo.com/3dc3063927860fb9d255496d51cf5637/thumb/1000)
![image](https://gyazo.com/3d98c29cec8322a89ab0b55f83a823a6/thumb/1000)

今日中に他人が触れる状態に持っていきたいね
- 静的生成してGitHub PagesするGitHub Actionsかな
- まあ、一旦は手動でもいいか
    - 手動って言ってもAIの手だが


これを「複数の章のファイルがあり、その中に複数のセクションがある」という一冊の書籍の原稿に使いたい
- 単純に全部を表示するのはインパクトはあるがユーザの利便性は悪いと思う
- どうするのがいいかの計画を立てよう


AIが勝手に全セクション統合を作ったがやっぱりダメダメだった
- ![image](https://gyazo.com/57627baef5a70a5bca517f02989ad084/thumb/1000)




ドラッグして離したらそのノードはpin止めされて位置が固定されるようにする

グラフをGPT5に渡して、章をまたいだキーワードの出現を見つけるのがよさそう
- それはつまり複数の章で語られるような重要な概念


個別の章のグラフでも連結になってないパターンがある
- 決めうちで10個の概念を抽出しているので足りないということ
- 間をつなぐ概念を見つけさせるのを別途やってもいいのかもな


章をまたいでいる参照も抽出できると面白い

---
全データ完了した
- $1


---
<img src='https://scrapbox.io/api/pages/nishio/Claude/icon' alt='Claude.icon' height="19.5"/>
⏺ 長い章データ処理時の挙動
1. 12,000文字で自動切り詰め (pipeline.py:151, 177行目)
- LLMへの送信時、sec.text[[:12000]]で最初の12,000文字のみ処理
- 残りのテキストは無視される

重大な問題を発見:
1. 2-0-ITと民主主義　拡大する溝.md
- Section 9: 25,515文字 → 53%が失われる
2. 3-3-失われた道.md
- Section 10: 16,308文字 → 26%が失われる
これらのセクションでは、重要な内容の半分以上（2-0の場合）が処理されていません。`sec.text[:12000]`による単純な切り詰
めは、文脈や重要な情報を失う可能性があります。

これすごい問題かと思ったが、ページ末に脚注がいっぱいついているだけだな<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>

---
連結でない章を連結にする作業
- [[連想接続]]そのものだな

![image](https://gyazo.com/c653ec9244d36e22b270920d47a81f61/thumb/1000)
できた
![image](https://gyazo.com/718eb1605c505b864832f96b8c08df68/thumb/1000)
うまく修復できている

孤立点ではないバージョン
![image](https://gyazo.com/441786e1b1e7738181fc1c2fc6979b63/thumb/1000)
![image](https://gyazo.com/6c98c1a69569b3314f9bbe6e22cd4b3a/thumb/1000)
なるほどね、「最新版の入手」と「非線形読書とハイパーリンク」の間に「オンライン版」が挿入されたのか。

ちなみにpromptの生成をするツールを作って必要な情報の全部入ったpromptを作り、ChatGPT 5 Thinkingに投げている

![image](https://gyazo.com/e94d9c5d52ab01e3de403b51a4ae262a/thumb/1000)

5-miniでもできるかな
- でも数件を僕がみながら投げるだけでできるから実装しなくてもいいかなという気もしてしまう
- "4-3の橋渡し概念は「小切手」です。"
    - 面白い

![image](https://gyazo.com/d3b9bb1df51aba6afb75bac8bd081333/thumb/1000)
- SNSノードを追加して接続

![image](https://gyazo.com/e252d0cfd47f2a1c1e8339498328614a/thumb/1000)
- これがどうにかなるのか楽しみ
- > 連結不足を埋める橋渡し概念を最小3個追加し、12本のエッジで全ノードが一つの主連結成分に統合される案です。
- ![image](https://gyazo.com/82903fdbe4b6d8d2b30b2b95b7e1a143/thumb/1000)
- つながった！

[[pConceptMap2025-09-10]]
