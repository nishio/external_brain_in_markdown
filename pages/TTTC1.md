---
title: "TTTC1"
---

:

```
2024-06-14 16:11:21,333 - BERTopic - Clustered reduced embeddings
Traceback (most recent call last):
  File "/Users/nishio/talk-to-the-city-reports/scatter/pipeline/main.py", line 39, in <module>
    main()
  File "/Users/nishio/talk-to-the-city-reports/scatter/pipeline/main.py", line 35, in main
    termination(config, error=e)
  File "/Users/nishio/talk-to-the-city-reports/scatter/pipeline/utils.py", line 295, in termination
    raise error
  File "/Users/nishio/talk-to-the-city-reports/scatter/pipeline/main.py", line 26, in main
    run_step('clustering', clustering, config)
  File "/Users/nishio/talk-to-the-city-reports/scatter/pipeline/utils.py", line 255, in run_step
    func(config)
  File "/Users/nishio/talk-to-the-city-reports/scatter/pipeline/steps/clustering.py", line 19, in clustering
    result = cluster_embeddings(
             ^^^^^^^^^^^^^^^^^^^
  File "/Users/nishio/talk-to-the-city-reports/scatter/pipeline/steps/clustering.py", line 65, in cluster_embeddings
    _, __ = topic_model.fit_transform(docs, embeddings=embeddings)
            ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/Users/nishio/talk-to-the-city-reports/scatter/venv/lib/python3.12/site-packages/bertopic/_bertopic.py", line 411, in fit_transform
    self._extract_topics(documents, embeddings=embeddings)
  File "/Users/nishio/talk-to-the-city-reports/scatter/venv/lib/python3.12/site-packages/bertopic/_bertopic.py", line 3295, in _extract_topics
    self.c_tf_idf_, words = self._c_tf_idf(documents_per_topic)
                            ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/Users/nishio/talk-to-the-city-reports/scatter/venv/lib/python3.12/site-packages/bertopic/_bertopic.py", line 3488, in _c_tf_idf
    self.vectorizer_model.fit(documents)
  File "/Users/nishio/talk-to-the-city-reports/scatter/venv/lib/python3.12/site-packages/sklearn/feature_extraction/text.py", line 1340, in fit
    self.fit_transform(raw_documents)
  File "/Users/nishio/talk-to-the-city-reports/scatter/venv/lib/python3.12/site-packages/sklearn/base.py", line 1152, in wrapper
    return fit_method(estimator, *args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/Users/nishio/talk-to-the-city-reports/scatter/venv/lib/python3.12/site-packages/sklearn/feature_extraction/text.py", line 1389, in fit_transform
    vocabulary, X = self._count_vocab(raw_documents, self.fixed_vocabulary_)
                    ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/Users/nishio/talk-to-the-city-reports/scatter/venv/lib/python3.12/site-packages/sklearn/feature_extraction/text.py", line 1295, in _count_vocab
    raise ValueError(
ValueError: empty vocabulary; perhaps the documents only contain stop words
```

