---
title: "We Have No Moat, And Neither Does OpenAI"
---

2021年の会話「[[機械学習は装置産業への揺り戻しか？]]」において、機械学習において大規模な装置を確保できる大企業が圧倒的に強く、この[[設備投資]]が中小規模の事業者が参入できない[[参入障壁]](Moat)となるのではと考えた。
これは大規模事業者内からの視点では「自社の技術を秘匿することによって市場での優位性が保てる」という仮説である。
しかし2023年5月時点で、[[LlaMa]]のリークと低コストな改良手法である[[LoRA]]の出現によって、Googleの優位性は脅かされていて、OpenAIも同様だ、という話。


2023/05/04 [Google "We Have No Moat, And Neither Does OpenAI"](https://www.semianalysis.com/p/google-we-have-no-moat-and-neither)
![image](https://gyazo.com/0b9aca56dea348239efd300e0cc74631/thumb/1000)

> Why We Could Have Seen It Coming
>  In many ways, this shouldn’t be a surprise to anyone. The current renaissance in open source LLMs comes hot on the heels of a renaissance in image generation. The similarities are not lost on the community, with many calling this the “[[Stable Diffusion moment]]” for LLMs.
- [[Stable Diffusion]]

>  In both cases, low-cost public involvement was enabled by a vastly cheaper mechanism for fine tuning called low rank adaptation, or [[LoRA]], combined with a significant breakthrough in scale ([[latent diffusion]] for image synthesis, [[Chinchilla]] for LLMs). In both cases, access to a sufficiently high-quality model kicked off a flurry of ideas and iteration from individuals and institutions around the world. In both cases, this quickly outpaced the large players.
- [[latent diffusion]] = [[latent diffusion model]]
- Chinchilla
    - [[Training Compute-Optimal Large Language Models]]


> The legal cover afforded by “personal use” and the impracticality of prosecuting individuals means that individuals are getting access to these technologies while they are hot.
- 「個人を訴追することの非現実性」これがキーだな


Timeline
> The Timeline
>  Feb 24, 2023 - [[LLaMA]] is Launched
>  Meta launches LLaMA, open sourcing the code, but not the weights. At this point, LLaMA is not instruction or conversation tuned. Like many current models, it is a relatively small model (available at 7B, 13B, 33B, and 65B parameters) that has been trained for a relatively large amount of time, and is therefore quite capable relative to its size.
>
>  March 3, 2023 - The Inevitable Happens
>  Within a week, LLaMA is leaked to the public. The impact on the community cannot be overstated. Existing licenses prevent it from being used for commercial purposes, but suddenly anyone is able to experiment. From this point forward, innovations come hard and fast.
- LLaMAがリークされた
- [[開放性]]が[[テクニウム]]を進歩させる

>  March 12, 2023 - Language models on a Toaster
>  A little over a week later, Artem Andreenko gets the model working on a Raspberry Pi. At this point the model runs too slowly to be practical because the weights must be paged in and out of memory. Nonetheless, this sets the stage for an onslaught of minification efforts.
>
>  March 13, 2023 - Fine Tuning on a Laptop
>  The next day, Stanford releases Alpaca, which adds instruction tuning to LLaMA. More important than the actual weights, however, was Eric Wang’s alpaca-lora repo, which used low rank fine-tuning to do this training “within hours on a single RTX 4090”.
>
>  Suddenly, anyone could fine-tune the model to do anything, kicking off a race to the bottom on low-budget fine-tuning projects. Papers proudly describe their total spend of a few hundred dollars. What’s more, the low rank updates can be distributed easily and separately from the original weights, making them independent of the original license from Meta. Anyone can share and apply them.
>
>  March 18, 2023 - Now It’s Fast
>  Georgi Gerganov uses 4 bit quantization to run LLaMA on a MacBook CPU. It is the first “no GPU” solution that is fast enough to be practical.
>
>  March 19, 2023 - A 13B model achieves “parity” with Bard
>  The next day, a cross-university collaboration releases Vicuna, and uses GPT-4-powered eval to provide qualitative comparisons of model outputs. While the evaluation method is suspect, the model is materially better than earlier variants. Training Cost: $300.
>
>  Notably, they were able to use data from ChatGPT while circumventing restrictions on its API - They simply sampled examples of “impressive” ChatGPT dialogue posted on sites like ShareGPT.
>
>  March 25, 2023 - Choose Your Own Model
>  Nomic creates GPT4All, which is both a model and, more importantly, an ecosystem. For the first time, we see models (including Vicuna) being gathered together in one place. Training Cost: $100.
>
>  March 28, 2023 - Open Source GPT-3
>  [[Cerebras]] (not to be confused with our own Cerebra) trains the GPT-3 architecture using the optimal compute schedule implied by Chinchilla, and the optimal scaling implied by μ-parameterization. This outperforms existing GPT-3 clones by a wide margin, and represents the first confirmed use of μ-parameterization “in the wild”. These models are trained from scratch, meaning the community is no longer dependent on LLaMA.
- [[Cerebras]]はLLaMaのリークモデルに依存しなくなった

>  March 28, 2023 - Multimodal Training in One Hour
>  Using a novel [[Parameter Efficient Fine Tuning]] (PEFT) technique, LLaMA-Adapter introduces instruction tuning and multimodality in one hour of training. Impressively, they do so with just 1.2M learnable parameters. The model achieves a new SOTA on multimodal ScienceQA.
>
>  April 3, 2023 - Real Humans Can’t Tell the Difference Between a 13B Open Model and ChatGPT
>  Berkeley launches Koala, a dialogue model trained entirely using freely available data.
>
>  They take the crucial step of measuring real human preferences between their model and ChatGPT. While ChatGPT still holds a slight edge, more than 50% of the time users either prefer Koala or have no preference. Training Cost: $100.
>
>  April 15, 2023 - Open Source RLHF at ChatGPT Levels
>  Open Assistant launches a model and, more importantly, a dataset for Alignment via RLHF. Their model is close (48.3% vs. 51.7%) to ChatGPT in terms of human preference. In addition to LLaMA, they show that this dataset can be applied to Pythia-12B, giving people the option to use a fully open stack to run the model. Moreover, because the dataset is publicly available, it takes RLHF from unachievable to cheap and easy for small experimenters.
