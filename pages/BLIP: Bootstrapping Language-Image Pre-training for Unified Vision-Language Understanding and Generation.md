
> Vision-Language Pre-training ([[VLP]]) has advanced the performance for many vision-language tasks. However, most existing pre-trained models only excel in either understanding-based tasks or generation-based tasks. Furthermore, performance improvement has been largely achieved by scaling up the dataset with noisy image-text pairs collected from the web, which is a suboptimal source of supervision. In this paper, we propose BLIP, a new VLP framework which transfers flexibly to both vision-language understanding and generation tasks. BLIP effectively utilizes the noisy web data by bootstrapping the captions, where a captioner generates synthetic captions and a filter removes the noisy ones. We achieve state-of-the-art results on a wide range of vision-language tasks, such as image-text retrieval (+2.7% in average recall@1), image captioning (+2.8% in CIDEr), and VQA (+1.6% in VQA score). BLIP also demonstrates strong generalization ability when directly transferred to video-language tasks in a zero-shot manner. Code, models, and datasets are released at this https URL.
[https://arxiv.org/abs/2201.12086](https://arxiv.org/abs/2201.12086)

ざっくり言えば
- 「ネット上の画像とその説明文のペアを収集して学習データに使う」というアプローチは説明文がしばしば適切でないのでノイジー
- 提案手法ではまず画像から説明文を作り、それとWeb上の説明文を比較して、より良い方を選ぶことで学習データを改善していく
    - ![image](https://gyazo.com/e177a0b5e05690359ace08067bd2b328/thumb/1000)

- Q: どうやって説明文を作るのか
- Q: どうやって「より良い説明文」かを判定するのか

github: [https://github.com/salesforce/BLIP](https://github.com/salesforce/BLIP)

[[BLIP]]