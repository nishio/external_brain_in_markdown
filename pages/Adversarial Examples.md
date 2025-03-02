
- 機械学習による画像分類を誤認識させる入力の作り方
- あるモデルでのAEは別のモデルでも誤分類されやすい
    - つまり自然界であまり出現しない事例になっているのでは

Transferability in Machine Learning: from Phenomena to Black-Box Attacks using Adversarial Samples
[https://arxiv.org/abs/1605.07277](https://arxiv.org/abs/1605.07277)
![image](https://gyazo.com/0cfa921d2c9d6a3306f04439d0edb48b/thumb/1000)
- 手元で作ったAEを別のモデルに食わせた時にどの程度攻撃が成功するか
- LRが意外と強い
    - 素朴な鈍器で殴るイメージ
- kNN強いのが面白い
    - 距離で判定するモデルを、距離に制限のついている摂動で騙すのだから、良いポイントを狙ってつく摂動が生成されているのだろう
