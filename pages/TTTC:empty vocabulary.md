---
title: "TTTC:empty vocabulary"
---

[[Talk to the City]]における未解決問題

僕は2024-09-11ごろ体験した
- [[TTTCをAzure OpenAIで使う]]のを試してコードを書き換えたりしている最中だったので自分の環境でだけ発生するものだと思っていた
2024-09-16
- [[proj-broadlistening]]で9/16に[[blu3mo]]から言及があり([link](https://cfj.slack.com/archives/C07JHK1M58A/p1726470787750939))、自分の環境以外でも発生することがわかった
2024-09-28
- [[TTTC:形態素解析]]
    - これが正攻法での解決方法だと思う
    - がしかしそもそもどういう時に発生するのかが謎
2024-10-29
- 2024-10-29現在は[[日テレNEWS×2024衆院選×ブロードリスニング]]のバージョンのソースコードが公開されてるのでそれを使うのが楽

わかっていることメモ

> ValueError: empty vocabulary; perhaps the documents only contain stop words
clusteringのここで発生する
:

```
    _, __ = topic_model.fit_transform(docs, embeddings=embeddings)
```


(9/11)返り値を使ってないように見えるがこの行自体は必要
- > Talk to the Cityの“BERTopicつかってないのでは？“という話に関して `_, __ = topic_model.fit_transform(docs, embeddings=embeddings)` をコメントアウトしたら下の `result = topic_model.get_document_infoで ValueError: This BERTopic instance is not fitted yet. Call 'fit' with appropriate arguments before using this estimator.` になったので使ってはいる、返り値を使わずにmodelの内部状態か更新されてるだけ(だったら`_, __ =`ってかかなくていいのに) ということがわかりました

(9/11)PDBで追いかけてみたが途中で断念
:

```
409             else:
410                  # Extract topics by calculating c-TF-IDF
411  ->             self._extract_topics(documents, embeddings=embeddings)
```


:

```
(Pdb) self._c_tf_idf(documents_per_topic)
*** ValueError: empty vocabulary; perhaps the documents only contain stop words
```


:

```
3485            if partial_fit:
3486                X = self.vectorizer_model.partial_fit(documents).update_bow(documents)
3487 ->         elif fit:
3488                self.vectorizer_model.fit(documents)
3489                X = self.vectorizer_model.transform(documents)
3490            else:
3491                X = self.vectorizer_model.transform(documents)

(Pdb) self.vectorizer_model.fit(documents)
*** ValueError: empty vocabulary; perhaps the documents only contain stop words
```


まあvectorizer_modelは下記なのでCountVectorizerがエラーを出しているのは間違いない
- [CountVectorizer — scikit-learn 1.5.2 documentation](https://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.CountVectorizer.html)
clustering.py

```
   CountVectorizer = import_module(
       'sklearn.feature_extraction.text').CountVectorizer
   ...
   vectorizer_model = CountVectorizer(stop_words=stop)
   
   topic_model = BERTopic(
       umap_model=umap_model,
       hdbscan_model=hdbscan_model,
       vectorizer_model=vectorizer_model,
       verbose=True,
   )
```


僕の手元のsklearn.__version__のバージョンは1.3.1だった

tokenizer.get_feature_names_outとかで使われてるfeaturesを見ると、もちろん日本語は単語に分けられてない
- defaultで`CountVectorizer(..., token_pattern='(?u)\\b\\w\\w+\\b')`なんだから当たり前だと思う
- むしろ安野都知事選のタイミングでなぜこれで動いてたのかわからない
    - 振り返ってみると6/9の僕のコメント:
        - > 元のソースはクラスタリング部分で英語を前提としたCountVectorizerを使ってるので僕の実験では(世界に向けて見せたかったこともあり)英語で抽出、英語でクラスタリングして結果を和訳したが、翻訳のクオリティの問題はあった。今回は日本人がターゲットなので日本語で抽出、日本語でクラスタリング、翻訳はなし、がいいのではないか。その場合は、クラスタリング部分でBag of Wordsしてるので、日本語の場合は形態素解析かキーワード抽出が必要
        - この後6/11に「日本語プロンプトでやってみたらできた」という報告があったので、時間もないから動くならそれでいいか、となった
        - 9/16のコメント
            - > そもそも論としてTTTCのメインの処理の部分は日本語を想定した実装になってなくてストップワードも英語だし形態素解析もしてない。英語でやって結果を和訳するか、日本語が通るように形態素解析を入れるかのどっちかが必要なのではという話になったのだけど、プロンプトを和訳したら問題なく動いたと報告があって、自分の手元でも追試したら確かに動いたので「じゃあいいかー」となった
            - >  動かない現状の方が僕の理解にマッチする振る舞い
- 単語に分割できない時に文字での分割にfallbackする仕組みがバージョンによっては入ってるとか？
    - いま(9/18)[CountVectorizer — scikit-learn 1.5.2 documentation](https://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.CountVectorizer.html#sklearn.feature_extraction.text.CountVectorizer.get_feature_names_out)を読んでたんだがdefaultのanalyzer='word'を'char'に変えたら動きそうではあるな
        - Bag of Charsでほんとにいいのかというのはさておき

9/16の投稿:
- 9/11の発生時はAzure関連だと思ってたので、ライブラリの依存関係を追うのが面倒で真面目な解決を諦めた
    - 代わりに抽出した日本語データに対して英訳を末尾につけるようにプロンプトを修正してワークアラウンドした
        - > 末尾に英語への翻訳をつけてください。
    - その方法でワークアラウンドできるということは日本語文章のトークナイズに関する問題だろうと思っててる

9/18
- 今現在の考えとしては`analyzer=‘char’`で動くのでは？と思っている
- 本質的にはちゃんと[[形態素解析]]すべきだと思う
    - CountVectorizerは関数を渡してoverrideできるのでその方法で。
