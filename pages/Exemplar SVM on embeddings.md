
> [@karpathy](https://twitter.com/karpathy/status/1647025230546886658?s=20): Random note on k-Nearest Neighbor lookups on embeddings: in my experience much better results can be obtained by training SVMs instead. Not too widely known.
> Short example:
> [https://t.co/RXO9xiOmAB](https://t.co/RXO9xiOmAB)
> Works because SVM ranking considers the unique aspects of your query w.r.t. data.
> [@phillip_isola](https://twitter.com/phillip_isola/status/1647053079487959046?s=20): @karpathy Neat! I think this is the same trick as studied in this great old paper? [https://t.co/TKOWZXc2V9](https://t.co/TKOWZXc2V9)
- [Ensemble of Exemplar-SVMs for Object Detection and Beyond](https://www.cs.cmu.edu/~tmalisie/projects/iccv11/)
> [@karpathy](https://twitter.com/karpathy/status/1647054838658924546?s=20): @phillip_isola Yep exactly! :) The first time I saw the [[Exemplar SVM]] idea. It's so simple but also a bit counter-intuitive, I think because low dimensional intuition fails us. A classifier with a single example? In low dimensions it sounds weird. In high dimensions it works great.


> [@olivkoch](https://twitter.com/olivkoch/status/1647213933646815234?s=20): @karpathy Nice. But you need to train an SVM for every query? Or did I miss something?
> [@karpathy](https://twitter.com/karpathy/status/1647278292490387456?s=20): @olivkoch yeah :D it's not as bad as it sounds, e.g. using the example in the notebook, training an SVM on ~10K 1536D embeddings is ~1 second. Sometimes it's possible to precompute. And sometimes it's just not worth it, all depends on setting / application.

> [@s_daptardar](https://twitter.com/s_daptardar/status/1647268625877962752): @karpathy @phillip_isola Exemplar SVM is great, but usually the problem is that the query has to be fast. Around the same time there was work on [[product quantization]] for approximate nearest neighbor search by Jegou, Douze et al which led to FAISS library. [https://t.co/tpjFwV8nG1](https://t.co/tpjFwV8nG1)
- [[Product quantization for nearest neighbor search]]
- Herve J ´ egou, Matthijs Douze, Cordelia Schmid
