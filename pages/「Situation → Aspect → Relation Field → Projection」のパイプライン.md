---
title: "「Situation → Aspect → Relation Field → Projection」のパイプライン"
---

<img src='https://scrapbox.io/api/pages/nishio/Karwi/icon' alt='Karwi.icon' height="19.5"/>
- このパイプラインは「普通のグラフモデル(まずノードを作って、後で関係で結ぶ)」と 順序が逆 という点が肝です。具体例で見せます。
- Situation
    - 未分節な状況。原文・会話・違和感・モヤモヤ。
    - まだ「何が項で何が関係か」分かっていない状態。
- Aspect
    - 持ち上げられた切り口。
    - 「ここに何かある」「似ている気がする」「Cが鍵?」
    - まだノードでもエッジでもない、注意の方向だけ。
- Relation Field
    - 側面をもとに、項・役割・文脈・根拠を持つ構造。
    - N項とは限らない。「まだ語がない」も保存できる。
- Projection
    - 画面上の見え方。線、カード、表、議論マップ、タイムライン、文章。用途に応じて切り替える。

1. 未分節な状況がある(原文・会話・違和感)
2. そこから何かが持ち上がる(=側面)
3. 側面を言うと、項が「立ち上がる」(まだ独立に存在していなかった)
4. 関係場として形がついてくる
5. それを必要に応じて線/表/カードに射影する

このパイプラインは「綺麗に4ステップで進む」ものではなく、行き来する:
- Aspect を持ち上げると Situation の見え方が変わる(Gendlin の carry forward)
- Relation Field を formulate しようとして「合わない」と分かると、Aspect Tray に新しい側面が増える
- Projection を切り替える(線→表→文章)と、Relation Field の弱点が見えて Aspect 層に戻る

Kozaneba の現状との対応
:
| Kozaneba の現状 | パイプライン上の位置 |
| -- | -- |
| こざねを書く | Situation(原文)を保持 |
| こざねを近くに置く | Aspect の暗黙的表現(空間配置で「何か似てる」を保持) |
| 線を引く | いきなり Projection(関係場をスキップ) |
| グループ化 | Aspect の半明示的表現 |
つまり Kozaneba は Situation Pad と Projection View の間に Aspect Tray と Relation Field がない ことが構造的特徴。だから「線を引く」=「関係場を経由せずに直接射影する」になっていて、関係の意味論が貧しいまま固定化される。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>KozanebaのこざねはScrapboxのページタイトルに相当するもので、現状のこざねは「ページ本文」に相当するものを持っていないように思う。一方でScrapboxの「ページタイトルとページ本文が1対1対応」もおかしくて、1つの長文からN個の短文(=タイトル/こざね)が生えていると思う
- <img src='https://scrapbox.io/api/pages/nishio/Karwi/icon' alt='Karwi.icon' height="19.5"/>梅棹忠夫のオリジナルの「[[こざね]]」は 複数の断片を綴じたもの(ホッチキスで束ねた紙きれのつらなり)で、Pipeline 上は Relation Field の formulation に近い。一方 Kozaneba の「こざね」は 個別の断片 で Aspect 寄り。
    - なるほど<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
- <img src='https://scrapbox.io/api/pages/nishio/Karwi/icon' alt='Karwi.icon' height="19.5"/>Scrapbox の実運用では、長文を書きながら bracket で囲んだ部分がタイトル化されて別ページに分かれていく — これがまさに「1 長文 → N タイトル」の現場。
- <img src='https://scrapbox.io/api/pages/nishio/Karwi/icon' alt='Karwi.icon' height="19.5"/>Roam / Logseq の block model: block transclusion で「1 long passage の中の N 個の block が他所から参照される」を実装。長文と短文の関係をデータ構造で保持
