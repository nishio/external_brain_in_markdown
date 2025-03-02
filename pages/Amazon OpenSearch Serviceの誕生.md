---
title: "Amazon OpenSearch Serviceの誕生"
---

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>OSS文脈におけるAmazonとElasticsearchの出来事を解説して

<img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>AmazonとElasticsearchの間には、[[オープンソースソフトウェア]]（OSS）の文脈で重要な出来事がありました。これは、特にAmazonがElasticsearchソフトウェアをベースにしたサービス「Amazon Elasticsearch Service」（現在のAmazon OpenSearch Service）を提供し始めたことに起因しています。以下、その経緯を簡潔に説明します。

- Amazon Elasticsearch Serviceの開始: [[Amazon Web Services]]（AWS）は、[[Elasticsearch]]という人気のあるオープンソースの検索エンジンを使用して、Elasticsearch Serviceを提供し始めました。このサービスは、クラウド上でElasticsearchを簡単にデプロイして運用できるようにするものでした。
- ライセンス変更: Elasticsearchは元々[[Apache 2.0]]ライセンスの下で配布されていましたが、Elastic NV（Elasticsearchを開発している企業）は、Amazonが自社のサービスでElasticsearchを商用利用することに対抗するため、2021年にライセンスを[[Server Side Public License]] (SSPL) に変更しました。このライセンス変更は、Amazonなどの大企業がElasticsearchのコードをそのまま使用して自社の製品を構築することを制限する目的がありました。
- Amazon OpenSearch Serviceの誕生: Elastic NVのライセンス変更に応じて、AmazonはElasticsearch 7.10とKibana 7.10のバージョンを最後に[[フォーク]]を実行し、「OpenSearch」という新しいプロジェクトを立ち上げました。これはApache 2.0ライセンスのもとで開発されており、ElasticsearchとKibanaのオープンソース版として機能します。
- 市場への影響と業界の反応: Elasticのライセンス変更とAmazonのフォークは、オープンソースコミュニティ内外で多くの議論を呼びました。一部では[[オープンソースの理念]]に反するとの意見もありますが、他方で、[[ビジネスモデル]]の保護と[[持続可能性]]を確保するための必要な措置と見る声もあります。

これらの出来事は、オープンソースソフトウェアを取り巻く法的、経済的な課題に光を当てるものであり、商用企業がオープンソースプロジェクトをどのように利用し、また、コントリビュートするかについて重要な事例となっています。
