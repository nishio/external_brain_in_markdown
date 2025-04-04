---
title: "✅チャットログからRegroupマップを生成"
---

![image](https://gyazo.com/83fec466aa6464fd5cc5672f74dd1f2b/thumb/1000)


from [[pKeicho]]
🤔チャットログからワンクリックでRegroupが開いて欲しい
- どうやるか
- サーバサイドでRegroupのマップデータを生成してから開く
    - [[✅PythonでRegroupのマップを作成]]
    - 画面構成案
        - [[Keichoのログから生成するRegroupマップの付箋レイアウト]]
    - [[Regroup変換を試す]]
    - [[✅選択したキーワードを付箋にする]]
    - [[✅一部の質問を簡潔に付箋にする]]
- ✅サーバで動くようにする
    - リンクサジェストのAPIサーバが全部やってしまえばよい
        - Firestoreから読んで書く
        - keichoのサーバの方がいいか？
        - むしろリンクサジェストをkeichoサーバに持ってくる？
        - 現状のRegroupエクスポートはリンクサジェストの成果を使ってない
        - スモールスタートでkeichoサーバでやる
        - リンクサジェストではなく、これ専用にHerokuでサーバ立ててた
    - 今はKeichoのサーバのリポジトリで作業している
        - IDがハードコードで、ローカルのログを読んで、固定のマップIDで出力してる
            - その方が実験には都合がいい
        - ✅これにIDをリクエストで受け取って、Firestoreから読んで、新規作成するパスを作る


- Keichoの側にはスピナーを置く
    - 完了したらURLコピーダイアログ
        - 非同期なのでタブを開くとブロックされるため
    - いや、メニューを押した時点でダイアログ表示、生成が終わったらURL表示、か
    - スピナーはなくていいか
    - ✅Keichoのメニューからマップ生成をトリガー

- これができるようになると、チャットログではなく単なる複数行テキストも入れたくなるな
    - [[🤔複数行テキストからRegroupマップを生成]]
