---
title: "Don't Retrieve, Navigate: Distilling Enterprise Knowledge into Navigable Agent Skills for QA and RAG"
---

[https://arxiv.org/abs/2604.14572](https://arxiv.org/abs/2604.14572)
<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>
この論文は、RAGを「検索して上位文書を渡す」仕組みとして見るのではなく、LLMエージェントに文書集合の“[[地図]]”を渡して、自分で辿らせるという提案です。タイトルの Don’t Retrieve, Navigate はかなりそのままで、「retrieve だけするな、navigate させろ」という主張です。
提案手法名は [[Corpus2Skill]] です。対象は主に企業内ナレッジベース、カスタマーサポート文書、FAQ、製品マニュアルのような、構造化されていないが一定のドメイン内にある文書集合です。

通常のRAGでは、ユーザ質問をベクトル化し、類似する文書やチャンクを上位k件取ってきて、LLMに渡します。著者たちは、これだとLLMは「返ってきた断片」しか見えず、文書集合全体がどう整理されているか、未探索の領域に何があるか、別の枝に関連情報があるかを判断できない、と指摘しています。
Agentic RAGならLLMが複数回検索できますが、それでも「どの検索語を投げるか」を手探りで決める必要があります。つまり、検索ツールはあるが地図はない。[[RAPTOR]]や[[GraphRAG]]のような階層・グラフ型手法も、階層を作ってはいるものの、多くの場合、推論時には依然として検索結果だけをLLMに渡すので、LLMが階層そのものを直接眺めて移動するわけではない、という整理です。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
「こういうデータにはうまくいかない」の話が面白い

うちのLLM Wikiの感想
> LLM-wiki のページ群は「短い・単一トピック・ラベルで弁別可能」に寄せて書かれているので、Corpus2Skill 的な navigate が効きやすい側のコーパス。逆に raw/papers/ の論文全文や raw/nishio-考える花火.1hop.txt のような長文ダンプは TechQA / CUAD 側に近く、ナビゲーションだけでは届かない。これが「raw を直接読ませず、wiki ページ経由で扱う」3層構造の正当化にもなっている。

Wikiにする過程で単一トピックになって、関連はリンクで表現する形に変わる、ってところに積極的な意味があるわけか〜

