---
title: "Scrapboxをブログとして使うと編集にためらいを感じる"
---

Scrapboxを「コンテンツが時系列に並んでいるブログ」として使っていると、過去の記事を編集することに抵抗を感じる
- 更新によって過去の記事が上がってくることが一般的なブログのメンタルモデルに一致しないため

この解決方法について

その1、Scrapboxの実装に手を加える場合
- ブログ的使い方をしているユーザが、自分のプロジェクトを他の人が見たときのソート順を「作成日時順」にできれば良い
- 現状、作成日時順のソートは存在するが、プロジェクトごとに設定することができない
    - ソート順の情報はプロジェクトではなくユーザに紐づいているから
- 案1: ソート順の情報をプロジェクトに紐づける
- 案2: ユーザとプロジェクトの掛け合わせに紐づける
    - ユーザごとにそれぞれのプロジェクトをどの順で表示するかを設定できる
    - プロジェクトごとに初期値を設定できるとなお良い
![image](https://gyazo.com/44fe18ab8795817618151a657fd8fc26/thumb/1000)
- 案2であれば、例えば僕個人はこのプロジェクトを更新日時順にしつつ、このプロジェクトを初めて見る人の初期値はMost Linkedにする、なんてことが可能になる
    - ブログ的用法の人に限らず有用ではある

その2、現状のScrapboxの機能のままなんとかする場合
- プロジェクトを2つに分ける
    - ![image](https://gyazo.com/0744937c9567f248ec1813548f5a715b/thumb/1000)
    - 現状のブログ的プロジェクトと別に、[[生きているテキスト]]のためのプロジェクトを作る
    - 便宜的に「下書きプロジェクト」と呼ぶ
        - 公開でも非公開でもいい
        - まず現状のブログ的プロジェクトをエクスポートし、下書きプロジェクトにインポートする
    - 新しい記事はまず下書きプロジェクトの側に書く
        - 下書きプロジェクトは更新日時の変化を気にせずに書き換える
    - 書き終わってからブログ的プロジェクトにコピペする
        - プログ的プロジェクトは、記事を入れたら、基本的には書き換えない
    - 更新日時順で見てほしい人にはブログ的プロジェクトを教える