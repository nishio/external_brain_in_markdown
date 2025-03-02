
> Denoising diffusion probabilistic models ([[DDPM]]s) have achieved high quality image generation without adversarial training, yet they require simulating a [[Markov chain]] for many steps to produce a sample. To accelerate sampling, we present denoising diffusion implicit models ([[DDIM]]s), a more efficient class of iterative implicit probabilistic models with the same training procedure as DDPMs. In DDPMs, the generative process is defined as the reverse of a Markovian diffusion process. We construct a class of non-Markovian diffusion processes that lead to the same training objective, but whose reverse process can be much faster to sample from. We empirically demonstrate that DDIMs can produce high quality samples 10× to 50× faster in terms of wall-clock time compared to DDPMs, allow us to trade off computation for sample quality, and can perform semantically meaningful image interpolation directly in the latent space.
[https://arxiv.org/abs/2010.02502](https://arxiv.org/abs/2010.02502)

- ![image](https://gyazo.com/595652fbd6ba206b07df700489c26470/thumb/1000)
- DDPM(Denoising diffusion probabilistic models)においてはマルコフ的に「1ステップのノイズ除去」を学習していたが、DDIM(denoising diffusion implicit models)ではそれを非マルコフ的にした
    - これによって10〜50倍くらい速くなった

[[Diffusion model]]

adversarial training: see [[GAN]]
