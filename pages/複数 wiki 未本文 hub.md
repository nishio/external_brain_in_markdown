---
title: "複数 wiki 未本文 hub"
---

<img src='https://scrapbox.io/api/pages/nishio/grasp/icon' alt='grasp.icon' height="19.5"/>
- これは、新しく入れた whole-store retrieval を実データで試した結果です。
- llm-wiki forest dogfood は、/Users/nishio/llm-wiki/wikis.yaml に登録されている複数 wiki を 1 つの grasp store に import して、project を指定せずに横断検索した、という意味です。結果として 42 個の wiki project、3,404 ページ、270,371 行、24,279 edge の森になりました。
    - このimportに4分弱だったらしい<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
- 「複数 wiki 未本文 hub」は「まだ独立ページとして書かれていないが、複数の wiki が同じ概念名を必要としている」候補です。
- 例
    - 狭義と広義
        - 複数 wiki に出現
        - 「同じ言葉が狭い意味と広い意味で使われる」問題の hub
    - アナロジー
        - 複数 wiki で参照されるが、少なくとも source 側では本文がない
        - 汎用概念なので、分野横断の接続点になりやすい
    - 利用と探索のトレードオフ
        - blindspot などから unresolved として出る一方、別 project の llm-wiki には materialized page がある
        - ここは今回の weak cross-project edge が効いて、blindspot -> llm-wiki の 1-hop path として見えた

- 重要なのは、「未本文」は必ずしも store 全体で本文が一切ないという意味ではありません。source project 内では赤リンクだが、別 project には同名ページがある場合があります。その時 grasp は authored なリンクを strong、名前一致で推論した横断接続を weak / inferred-normalized-title として出します。
- なので今回確認できた価値は、「複数 wiki に散っている赤リンク概念」と「別 wiki にある既存本文」を同じ graph surface で見られるようになったことです。これは単一 project の Cosense では見えにくい、forest 向けの本命シグナルです。