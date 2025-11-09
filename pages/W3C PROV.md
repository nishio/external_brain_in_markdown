---
title: "W3C PROV"
---

<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>
以下だけ押さえればOKです。

要点
- W3C PROVは「[[来歴]]（[[provenance]]）」を共通フォーマットで表すための標準ファミリー。データや成果物が**誰（Agent）**によって、**どんな活動（Activity）**を経て、**どの実体（Entity）**になったかを記述します。信頼性評価・再現性・監査・データ系のトレーサビリティに使われます。([W3C](https://www.w3.org/TR/prov-overview/?utm_source=chatgpt.com))

中核の概念（3つ）
- Entity: ある時点の「もの／データ」。
- Activity: 何らかの処理・操作（開始/終了時刻を持てる）。
- Agent: 人・組織・ソフト等で、Activityに関わった主体。
代表的な関係: `wasGeneratedBy`（生成）、`used`（使用）、`wasDerivedFrom`（派生）、`wasAttributedTo`（帰属）、`wasAssociatedWith`（関連付け）、`actedOnBehalfOf`（代行）。([W3C](https://www.w3.org/TR/prov-dm/?utm_source=chatgpt.com))

仕様ファミリー（どれを読む/使う？）
- PROV-PRIMER（入門・まずこれ）([W3C](https://www.w3.org/TR/prov-primer/?utm_source=chatgpt.com))
- PROV-DM（概念モデルの定義）([W3C](https://www.w3.org/TR/prov-dm/?utm_source=chatgpt.com))
- PROV-N（人が読み書きしやすい記法）([W3C](https://www.w3.org/TR/prov-n/?utm_source=chatgpt.com))
- PROV-O（OWL2/RDFのオントロジー。Linked DataやSPARQL向け）([W3C](https://www.w3.org/TR/prov-o/?utm_source=chatgpt.com))
- PROV-XML（XMLスキーマ）、PROV-AQ（来歴の取得API/リンク指針）、PROV-Constraints（妥当性制約）([W3C](https://www.w3.org/TR/prov-aq/?utm_source=chatgpt.com))
- PROV-JSON（W3Cメンバー提出・勧告ではないが実務で利用例あり）([W3C](https://www.w3.org/Submission/prov-json/?utm_source=chatgpt.com))

ミニ例

PROV-N
provn

```
document
  prefix ex <http://example.com/>

  entity(ex:cleaned_csv)
  entity(ex:raw_csv)
  activity(ex:cleaning, 2025-09-01T12:00:00Z, 2025-09-01T12:05:00Z)
  agent(ex:alice)

  used(ex:cleaning, ex:raw_csv)
  wasGeneratedBy(ex:cleaned_csv, ex:cleaning)
  wasAssociatedWith(ex:cleaning, ex:alice)
  wasAttributedTo(ex:cleaned_csv, ex:alice)
endDocument
```

（構文の詳細は PROV-N 参照。RDFで使うなら下のPROV-Oへ。）([W3C](https://www.w3.org/TR/prov-n/?utm_source=chatgpt.com))

PROV-O（Turtle）
turtle

```
@prefix prov: <http://www.w3.org/ns/prov#> .
@prefix ex:   <http://example.com/> .

ex:cleaned_csv a prov:Entity ;
  prov:wasGeneratedBy ex:cleaning ;
  prov:wasAttributedTo ex:alice .

ex:raw_csv a prov:Entity .

ex:cleaning a prov:Activity ;
  prov:used ex:raw_csv ;
  prov:startedAtTime "2025-09-01T12:00:00Z"^^xsd:dateTime ;
  prov:endedAtTime   "2025-09-01T12:05:00Z"^^xsd:dateTime ;
  prov:wasAssociatedWith ex:alice .

ex:alice a prov:Agent .
```

（語彙やモデリング指針は PROV-O を参照。）([W3C](https://www.w3.org/TR/prov-o/?utm_source=chatgpt.com))

実務Tips
- RDF基盤があるなら PROV-O を採用（SPARQLで追跡・可視化しやすい）。軽量クライアント間交換なら PROV-JSON/JSON-LD 系も検討（ただし標準の地位は異なる）。([W3C](https://www.w3.org/TR/prov-o/?utm_source=chatgpt.com))
- API設計では、リソースから来歴へのリンクや取得方法に PROV-AQ を利用。([W3C](https://www.w3.org/TR/prov-aq/?utm_source=chatgpt.com))
- 整合性チェックや論理推論を意識するなら PROV-Constraints のルールを満たす。([W3C](https://www.w3.org/TR/prov-constraints/?utm_source=chatgpt.com))
- 変換/検証ツールやライブラリ（JavaのPROV Toolbox等）も公開されています。([openprovenance.org](https://openprovenance.org/service/about.html?utm_source=chatgpt.com))
必要なら、あなたのデータモデルに合わせた最小サブセット設計や**スキーマ（SHACL）**も一緒に切っていきます。

