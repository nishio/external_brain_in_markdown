---
title: "pScaffoldNetwork 2022-05-09"
---

[[足場ネットワーク]]2022-05-09 #pScaffoldNetwork
MeCabの制約付き解析
- 苦戦中
- 範囲外アクセスが起きる
    - 接尾辞配列の末尾より先を読もうとする
- 原因はまたわからない
- とりあえずプログラムが死なないようにワークアラウンドした場合、最後まで走り切る
- ただし表記揺れリンクが変
    - 冒頭単語は確かに共通
    - 末尾の単語も共通になるはずだがまちまち
- 出力結果をざっと見て、文章が復元されずに壊れてるとかはなさそうなので前進はしてるのだが
- 「範囲外アクセス」「表記揺れリンクが変」の原因が共通である可能性がある
    - 終わりの位置が1つズレているとか
        - それによって範囲外アクセスし、また表記揺れの末尾もおかしくなる
    - 単に最後の単語が欠けてるとかではないようだ、次の単語がイコールではない

大規模な重複文章があるデータの場合
- 例えば文章を推敲してバージョン違いでいくつもあるなどのケース
- 複数の文書を跨いだ長い共通文字列があるのでそれがキーワードだと判断してしまう
- 解決案
    - 特定の文書集合の間に大量の共通文字列リンクが発見されることになる
    - A: それを検知してスコアを減らす
    - B: 1つ抽出した上で「つなぐページの集合」がそれと被るものは抽出しないように読み飛ばす
        - クローン文章間だけに発生する超長いキーワードは、他の文書には出ないだろうからこれでフィルターできると思う
    - C: このようなものが自然に低スコアになるようなスコア計算式に変える
- そもそも論の話
    - 完全一致部分文字列なのか曖昧一致なのか区別せずにキーワードのスコアづけをしているが、そこを変える案もある
        - 今は区別してないので、変に表記揺れキーワードができると、だいたいそれは長いので、高いスコアになってしまう
            - 変になったときの挙動をよくするのはおかしいのでは、変にならないようにすべき
        - たとえそれをやっても「推敲を繰り返してバージョン違い文章を含んだデータ」では長い文字列一致が発生することは同じ
- 重複がないであろう別のデータセットを使って「MeCab制約付き解析」の部分の動作テスト
    - ここがまだうまく動いていない

どのようなリンクを選択するか？
- シンプルに各ページでスコアトップN案
    - 上位のキーワードでリンクされているページ集合と同一のものは除く案
    - 「既にリンクされてるページ」を持ち、包含されてるならスキップする案
        - Scrapboxの挙動に近い
    - ✅上位キーワードと文字列上でオーバーラップするものを除外
- スコアの高いリンクから1つずつ追加していく
    - Spanning Tree的発想

実験データ案
- 西田幾多郎PDFからインポートして公開
    - 哲学概論
- ドラッカー書籍から1冊インポート
    - これは非公開
    - OCRなのでうまくいかない可能性
- Scrapboxからの変換
    - dry-runで変換候補を出して、確認してからそれを元に変換
        - 候補をファイルに出して編集できるようにする？
- ネット上のコラム集などをクロールする案
