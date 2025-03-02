---
title: "FineWeb"
---

<img src='https://scrapbox.io/api/pages/nishio/Claude/icon' alt='Claude.icon' height="19.5"/>
FineWebは、2013年から2024年までのCommon Crawlのデータを15兆トークンにフィルタリングと重複排除したウェブデータセットです。FineWebで学習したモデルは、RefinedWeb、C4、DolmaV1.6、The Pile、SlimPajamaを上回る性能を示しました。

開発チームは、処理方法の意思決定を検証するために200以上のアブレーションモデルを学習し、セットアップを再現するために必要なコードをすべて共有しています。

FineWebは、データの質と多様性を重視しており、単なる大規模なデータセットではありません。開発チームは、H100クラスタで約12万GPU時間を費やし、アブレーションモデルを使用してデータの品質を評価しました。

2022年から2023年にかけて、アダルトコンテンツのドメインを強くフィルタリングしたため、Common Crawlの「LLMの品質」が大幅に低下するという直感に反する挙動も観察されました。

今後、フィルタリングの改善や多言語対応など、FineWebを継続的に改良していく予定です。また、実験から得られた生データを公開し、データフィルタリングの理解を深める取り組みも行う予定です。

> [gui_penedo](https://twitter.com/gui_penedo/status/1781953413938557276/photo/1) We have just released  FineWeb: 15 trillion tokens of high quality web data.
>  We filtered and deduplicated all CommonCrawl between 2013 and 2024.
>  Models trained on FineWeb outperform RefinedWeb, C4, DolmaV1.6, The Pile and SlimPajama!
>  ![image](https://gyazo.com/18304a4b7e981777e735517d6b626ec3/thumb/1000)
> [gui_penedo](https://twitter.com/gui_penedo/status/1781953418002870752) We trained 200+ ablation models to validate our processing decisions, and we share all the code you need to reproduce our setup, along with our dataset comparison ablation models checkpoints!
>  Find out all abut  FineWeb on the  model page:
>  [HuggingFaceFW/fineweb · Datasets at Hugging Face](https://huggingface.co/datasets/HuggingFaceFW/fineweb)

> [Thom_Wolf](https://twitter.com/Thom_Wolf/status/1781953413938557276/photo/1) Llama3 was trained on 15 trillion tokens of public data. But where can you find such datasets and recipes??
>
>  Here comes the first release of Fineweb. A high quality large scale filtered web dataset out-performing all current datasets of its scale. We trained 200+ ablation models to craft this dataset carefully parsing and filtering Common Crawl.
>
>  All recipes, data, ablations models, hyper-parameters are open-source and we plan to improve Fineweb over time so stay tuned for future versions.
>
>  Finally we made a number of surprising observations along the way (all Common crawl years are not equal, the influence of ChatGPT in latest webdata, etc) that we’re compiling in a longer tech blog post to be released in the coming days for the fine data lovers.
>
>  Enjoy

> [edunov](https://twitter.com/edunov/status/1781956600724345190) People seem to over-index on the 15T number after Llama 3. While the number matters, what is even more important is the quality and diversity of those tokens. If there was a good way to measure those, that would have been an impressive result to report.

> [Thom_Wolf](https://twitter.com/Thom_Wolf/status/1782691683517305226) This take on the FineWeb release is one of the most interesting feedback and also a reason FineWeb is very different from even larger datasets like RedPajama-V2 (which is double its size!)
>
>  Surprisingly, the size of the dataset of 15T tokens is not very important, what is much more important is why we spend ~120k GPU hours on the H100 cluster to prepare/share a ... dataset?
>
>  Let's take a moment to dive in it!
>
>  First, where can you get data at scale for web-scale llm pretraining? Well we're all lucky that Common Crawl is there and has been doing in the open a large chunk of the work of crawling/archiving the web for years, work that otherwise only private teams like Google/Bing would have access to.
>
>  Next question: can you just train directly on the petabytes common crawl corpus, maybe just extract the text from the html pages and train on it, the model will figure it out? You would have one of the largest possible dataset for sure!
>
>  The answer me and a part of the Mistral team who participated in BigScience/Bloom training learned over time is: No!
>
>  Like Sergey says below, you actually want a dataset which is both large but also high quality
>
>  What is high quality for a web-scale LLM pretraining dataset and how do you know you have it? Maybe I should then just train on, like, wikipedia only! The answer to this is also no. First because wikipedia is too small ofc but more important because our intuitive notion of data quality is not always reflected in the performance of the models and some aspects of data filtering can be counter-intuitive.
>
>  Before I dive more in this let me give you an example of unintuitive behavior. Between 2022 and 2023 the "LLM quality" of Common Crawl dropped significantly as in "training a LLM on the crawls btw 2022-2023 will give you lower performances on a set of evals". What happened? Well it turns out the Common Crawl team has been filtering more strongly domains with adult content. Not really the cause you'd be intuitively thinking about, right?
>
>  So how do you know you have good quality data? Well the simple, kinda circular, answer is: you just train on it. You train smaller models so it's not (too) expensive but still models that are big enough and on sensitive enough evaluations to give you signal about the quality of a larger model trained on the same dataset: this is what we call ablation models in FineWeb.
>
>  Which ablation models did we used? We settled on two ways of training ablation models: in the first option we trained a 1.8B parameters model on 28B tokens which took about 5h on 64 H100. In the second option we trained the same 1.8B params models but much longer, for 350B tokens (which took about 2.5 days on 64 H100). Note that in this second, larger, ablations we trained on more tokens than GPT3 or Bloom were trained for instance.
>
>  For each of many options for the filters we explored (heuristics and ML models), we trained some of these ablation models and compared the performance of the models to see if we saw an improvement or regression. Overall we trained about 200 small ablation and 15 larger ones for a total of more than 120k GPU hours.
>
>  You can see the results of these evaluations for instance in the performance plots we include in the dataset card where we train on 350B tokens (160k steps).
>
>  Overall this is the main difference with a simple raw Common Crawl and RedPajama-V2. In these later case you still need to do the work of selecting how to filter the data yourself and it's the work we wanted to provide the community with in FineWeb.
>
>  At least a first version of it since we see FineWeb as a ressource we will improve over time along various direction. Even better filtering for sure and also multilinguality which is very interesting as well.
>
>  To finish, an important parallel work I really need to mention is the work of the Dolma team which have been working tirelessly on improving the filtering of Dolma and, in our on-going training we see that the very latest release of Dolma from last week is very promising. We'll include these numbers in the coming blog post that we are currently writing and we are super happy about the work of the AllenAI team. Excited to dive in your dataset as well, friends!
>
>  Stay tuned for the blog post detailing all I mentioned above and other anecdotes in greater details!
>
>  Cheers

> [gneubig](https://twitter.com/gneubig/status/1782721111391666533) Wow, this is fascinating, thanks for sharing! If you would be willing to release the raw data from all of these experiments, it could be a really great resource to improve understanding of how we should be doing data filtering.

> [Thom_Wolf](https://twitter.com/Thom_Wolf/status/1782736947439382973) yes that's the goal, we're in the process of organizing all the artifacts and it should come out in the coming days with a more detailed tech report/blog

