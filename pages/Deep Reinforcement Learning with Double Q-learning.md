---
title: "Deep Reinforcement Learning with Double Q-learning"
---

Hado van Hasselt, Arthur Guez, David Silver
- 一般的な[[Q学習]]は特定のシチュエーションで行動価値を過大評価する
- こういうことがよく起こるのか、パフォーマンスに悪影響があるのか、防ぐことができるのか
- [[DQN]]はAtari 2600の一部ゲームで過大評価の影響を強く受ける
- Double Q-Learning
- 過大評価を抑制して、パフォーマンスが良くなる
- [https://arxiv.org/abs/1509.06461v3](https://arxiv.org/abs/1509.06461v3)
