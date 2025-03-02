---
title: "pVectorSearch2023-06-20"
---

from [[pVectorSearch]]
pVectorSearch2023-06-20
新機能案
GETでURLフラグメントにScrapboxのページ名を渡す
- Scrapbox側は新しいタブで開くUserScriptを作る
- 受け取った側はクライアントJSでAPIを叩いて、クエリに積んで検索を掛ける
- これで任意の公開プロジェクトから「ベクトル検索関連ページ」ができる
- 検索履歴に内容が丸ごと乗るのはうざい

- 僕の手書きの図があるページから図だけ検索したいな
- 同一ページ内のヒットを除外する方がデフォルトでいい気がしてきた

新UI案
![image](https://gyazo.com/6e99c7cd8a3697961f317e54a3ffb928/thumb/1000)
- +はallで-はnoneです
    - 2023/6/26　いや説明しないと意味わからんからallとnoneって書けばいいじゃん

2023/6/20
出張中のスマホからの検索でエラーになった
- その場では対処ができず今確認した
- 問題が再現しない
- Vercelの無料版なのでログは最大1時間らしい、もう何がエラーになったのかわからない
とりあえず問題なく動いてそうなので今回はパス
- ネクストアクション的にはSentry導入かな

新機能案
- 検索結果から「それを積んでプロンプト実行」を可能にする
    - ダイジェスト
    - ロールプレイ

2023-06-21
- client side
    - `Unexpected token 'A', "An error o"... is not valid JSON`
    - `Failed to load resource: the server responded with a status of 504 ()`
- server side:
    - `[POST] /api/search`
    - `Execution Duration / Limit 10.01s / 10s (timed out)`
- 単純にタイムアウトですな
    - タイムアウトの時のエラーメッセージを改善するとか、リトライするとかがネクストアクションかな

2023/6/26
- 自分が非公開ソースを含めて検索した上で、それを含んだ検索結果をうっかりシェアする未来が見えた
    - 非公開ソースを含んでるならシェアボタンを出さないようにしよう

2023/6/27
- エクスポート権限があることを前提に自動的にアップデートする仕組みを作る
- 今のソースをフォークして[/omoikane](https://scrapbox.io/omoikane)特化版をつくる
- 新しく作る
    - [[pVectorSearch2023-06-05]]を参考に
- 実験をしながら積み上げてるせいでソースコードがあちこちに散乱してるなぁ
    - 我ながら酷い
    - たまに整理しないと行方不明になる
- etude-github-actionsリポジトリからexportのコードを複製
- qdrantリポジトリから
    - pip freezeしてなかった
        - `$ pip install -r requirements.txt `
    - make_index_from_scrapbox.py
        - embedできた
        - [[Git LFS]]でキャッシュを保存
    - from_pickle_to_qdrant.py
        - qdrantに送るのもできた
        - コレクション名はomoikaneにした
            - 他の横断検索と一緒にするかどうか少し迷ったんだけど、わけとけば依存関係が少なくて話がシンプルなので
- nishio-vecsearchからUI周り
    - 不必要な機能を削り落としてシンプルにする
- デプロイ
    - あっ、しまった、データを突っ込む部分とサーバ実装は分けるべきだったか
    - Github Actionでデプロイが走ってしまう
    - そもそもエクスポート用のTSを見てVercelが混乱してる
        - あーあ
- 素直に分けるべきか
    - ベクトルを入れるomoikane-embedと検索するomoikane-vecsearch
- できた✅

2023-06-28
- Omoikane Embed、100トークンで刻む機能を追加したら同じページからの重複ヒットが多くなったなぁ
- 元に戻すのは簡単だが面白くない
- 同一ページからは1件だけ取るようにするか
- とか思ってたけど刻む方のコードをコミットし忘れてたので勝手に戻ってた、じゃあまあいいか

