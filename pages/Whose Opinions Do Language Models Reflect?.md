---
title: "Whose Opinions Do Language Models Reflect?"
---

LLMは[[RLHF]]によって高所得、高学歴、リベラルに近い意見を持つようになる
- なぜならその反対の人たちはRLHFに参加しないから
- LLMに対してHuman Feedbackを返さないことは、将来において自分の所属する意見集団が不利になる効果をもたらす

> Language models (LMs) are increasingly being used in open-ended contexts, where the opinions reflected by LMs in response to subjective queries can have a profound impact, both on user satisfaction, as well as shaping the views of society at large. In this work, we put forth a quantitative framework to investigate the opinions reflected by LMs -- by leveraging high-quality public opinion polls and their associated human responses. Using this framework, we create OpinionsQA, a new dataset for evaluating the alignment of LM opinions with those of 60 US demographic groups over topics ranging from abortion to automation. Across topics, we find substantial misalignment between the views reflected by current LMs and those of US demographic groups: on par with the Democrat-Republican divide on climate change. Notably, this misalignment persists even after explicitly steering the LMs towards particular demographic groups. Our analysis not only confirms prior observations about the left-leaning tendencies of some human feedback-tuned LMs, but also surfaces groups whose opinions are poorly reflected by current LMs (e.g., 65+ and widowed individuals).
- [https://arxiv.org/abs/2303.17548](https://arxiv.org/abs/2303.17548)
- [https://hai.stanford.edu/assets/files/2023-09/Opinions_PolicyBrief_9.2023_v3.pdf](https://hai.stanford.edu/assets/files/2023-09/Opinions_PolicyBrief_9.2023_v3.pdf)

(DeepL) 言語モデル(LM)は、主観的なクエリに対してLMが反映する意見が、ユーザの満足度に大きな影響を与えるだけでなく、社会全体の意見を形成することもある。本研究では、質の高い世論調査と、それに関連する人間の反応を利用することで、LM が反映する意見を定量的に調査する枠組みを提案する。このフレームワークを用いて、中絶からオートメーションまで幅広いトピックについて、LMの意見と米国の60の人口統計グループの意見の整合性を評価するための新しいデータセットであるOpinionsQAを作成した。各トピックにおいて、現在のLMが反映する意見と米国の人口統計グループの意見との間には、気候変動に関する民主党と共和党の対立に匹敵するほどの大きなズレがあることがわかった。特筆すべきは、このズレは、LMを特定の人口統計集団に明示的に誘導した後でも続いていることである。この分析は、人間のフィードバックによって調整されたLMの左寄りの傾向に関する先行研究を裏付けるだけでなく、現在のLMでは意見が反映されにくいグループ（65歳以上や寡婦など）を浮き彫りにするものでもある。

![image](https://gyazo.com/494da8d1ac100649e3db58eb894ff6fa/thumb/1000)

