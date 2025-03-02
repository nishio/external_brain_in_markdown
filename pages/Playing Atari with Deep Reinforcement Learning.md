
2013年の論文で、コンピュータにATARIのゲームをさせるもの。ゲームごとにアルゴリズムを調整したりせず単一の方法でチャレンジして3つのゲームで人間のエキスパートを超えた。
[https://arxiv.org/abs/1312.5602](https://arxiv.org/abs/1312.5602)

[[Paper Digest]]してみた
What this paper is about
- Introduction and Objective
    - This paper demonstrates that a convolutional neural network can overcome these challenges to learn successful control policies from raw video data in complex RL environments.
    - To alleviate the problems of correlated data and non-stationary distributions, we use ar X iv :1 31 2. 56 02 v1 [ cs.
    - Our goal is to create a single neural network agent that is able to successfully learn to play as many of the games as possible.
    - Recent advances in deep learning have made it possible to extract high-level features from raw sensory data, leading to breakthroughs in computer vision and speech recognition.
    - Furthermore, in RL the data distribution changes as the algorithm learns new behaviours, which can be problematic for deep learning methods that assume a fixed underlying distribution.
- What you can learn
    - Results
    - Discussion and Conclusions
        - This paper introduced a new deep learning model for reinforcement learning, and demonstrated its ability to master difficult control policies for Atari 2600 computer games, using only raw pixels as input.
        - We also presented a variant of online Q-learning that combines stochastic minibatch updates with experience replay memory to ease the training of deep networks for RL.
        - Our approach gave state-of-the-art results in six of the seven games it was tested on, with no adjustment of the architecture or hyperparameters.