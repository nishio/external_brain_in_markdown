
![image](https://gyazo.com/2d012ca999f667b2ba0210021d740338/thumb/1000)
[[Stable Diffusion]]の仕組み

> By decomposing the image formation process into a sequential application of denoising autoencoders, diffusion models (DMs) achieve state-of-the-art synthesis results on image data and beyond. Additionally, their formulation allows for a guiding mechanism to control the image generation process without retraining. However, since these models typically operate directly in pixel space, optimization of powerful DMs often consumes hundreds of GPU days and inference is expensive due to sequential evaluations. To enable DM training on limited computational resources while retaining their quality and flexibility, we apply them in the latent space of powerful pretrained autoencoders. In contrast to previous work, training diffusion models on such a representation allows for the first time to reach a near-optimal point between complexity reduction and detail preservation, greatly boosting visual fidelity. By introducing cross-attention layers into the model architecture, we turn diffusion models into powerful and flexible generators for general conditioning inputs such as text or bounding boxes and high-resolution synthesis becomes possible in a convolutional manner. Our latent diffusion models (LDMs) achieve a new state of the art for image inpainting and highly competitive performance on various tasks, including unconditional image generation, semantic scene synthesis, and super-resolution, while significantly reducing computational requirements compared to pixel-based DMs. Code is available at this https URL .
[https://arxiv.org/abs/2112.10752](https://arxiv.org/abs/2112.10752)

> 拡散モデル（DM）は、画像形成プロセスをノイズ除去オートエンコーダの逐次適用に分解することで、画像データおよびそれ以上のデータに対して最先端の合成結果を達成することができます。さらに、その定式化により、再トレーニングを行わずに画像生成プロセスを制御するためのガイド機構を実現することができる。しかし、これらのモデルは一般的にピクセル空間で直接動作するため、強力なDMの最適化はしばしば数百GPU日を消費し、逐次評価による推論も高価である。DMの品質と柔軟性を維持しつつ、限られた計算資源でDMの学習を可能にするために、我々は強力な事前学習済みオートエンコーダの潜在空間においてDMを適用する。従来の研究とは異なり、このような表現で拡散モデルを学習することで、複雑さの軽減とディテールの保存の間の最適なポイントに初めて到達し、視覚的忠実度を大幅に向上させることが可能となった。また、モデルアーキテクチャにクロスアテンションレイヤーを導入することで、拡散モデルをテキストやバウンディングボックスなどの一般的な条件入力に対する強力かつ柔軟な生成器とし、畳み込み方式で高解像度合成を可能にします。私たちの潜在的拡散モデル（[[LDM]]）は、ピクセルベースのDMと比較して計算量を大幅に削減しながら、画像インペインティングのための新しい技術水準と、無条件画像生成、意味的シーン合成、[[超解像]]を含む様々なタスクで高い競争力を達成しました。コードは、このhttpsのURLから入手できます。

- 拡散モデルとは、画像形成プロセスをノイズ除去オートエンコーダの逐次適用に分解すること
- > 再トレーニングを行わずに画像生成プロセスを制御するためのガイド機構を実現することができる
    - テキストプロンプトで生成される画像をコントロールする話
- これをピクセル空間で行うと高コスト
    - そこで潜在ベクトル空間で行う
    - ![image](https://gyazo.com/97dccbab020e9d43e0e0a152051d5325/thumb/1000)



- > モデルアーキテクチャに[[クロスアテンション]]レイヤーを導入することで、拡散モデルをテキストやバウンディングボックスなどの一般的な条件入力に対する強力かつ柔軟な生成器とし、畳み込み方式で高解像度合成を可能にします。

