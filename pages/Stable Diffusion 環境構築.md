
[[Stable Diffusion]]


2022-09-22
[[WSL2にMacからSSHする]]

stable diffusionをチェックアウトしたコードがAとBの二つあり、Aでconda環境を作った後で、Bで実験をしようとした
- 運用環境と実験環境と思って良い
- 実験環境でソースを編集したのになぜか読まれない

回答編
- `$ conda env create -f environment.yaml`
- これの中で`pip -e .`しているのでAがライブラリパスに入っており、インポートもAからされる
- 実験環境用に別の名前のconda環境を作った



--- old log 1
Windows向けの全部入りrar
- [https://grisk.itch.io/stable-diffusion-gui](https://grisk.itch.io/stable-diffusion-gui)
- 解凍してexeを実行するだけでGUIで使える
- これを昨日の夜、とりあえずゲーミングPCに入れてみた
    - 1枚40秒前後で作れる
    - [[日記2022-08-25]]

ゲーミングPCは開発環境が入ってない
- 「WSL 使い方」でググるところから…
- 「ストアからUbuntuを入れればいい」というのを間に受けたら折り畳まれた表示の中で「wslがオンになってない」と警告を出して止まってた
    - やたら時間がかかるなと思って詳細表示にして初めて気づいた
- 管理者権限のコマンドプロンプトからwsl --installしたら素直にインストールが始まった
- [https://github.com/CompVis/stable-diffusion](https://github.com/CompVis/stable-diffusion)
    - GPUに10GBのVRAMが必要と書いてあるが、まず自分が条件を満たしてるのか知らない
    - 調べ方を調べる
        - Win-R [[dxdiag]]
            - ![image](https://gyazo.com/7dc99a5760ace58f1c0d2205d6cf59ca/thumb/1000)
            - 8GBしかないように見えるが…w
    - Linux版Anacondaをインストールして
        - `$ conda env create -f environment.yaml`
        - `$ conda activate ldm`
        - LDM: [[latent diffusion model]]
    - [[Hugging Face]] からsd-v1-4.ckptをダウンロードする
        - [https://huggingface.co/CompVis/stable-diffusion-v-1-4-original](https://huggingface.co/CompVis/stable-diffusion-v-1-4-original)
    - `$ python scripts/txt2img.py --prompt "cat" --plms --ckpt sd-v1-4.ckpt`
        - `RuntimeError: No CUDA GPUs are available`
        - 🤔

Troubleshooting

:

```
$ nvidia-smi
Fri Aug 26 21:21:14 2022
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 495.47       Driver Version: 496.76       CUDA Version: 11.5     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  On   | 00000000:01:00.0 Off |                  N/A |
| N/A   52C    P8     6W /  N/A |    111MiB /  8192MiB |     N/A      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|  No running processes found                                                 |
+-----------------------------------------------------------------------------+
```

WSL環境はGPUのハードウェアを認識している

::

```
Python 3.8.5 (default, Sep  4 2020, 07:30:14)
[GCC 7.3.0] :: Anaconda, Inc. on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import torch
>>> torch.version.cuda
'11.3'
>>> torch.cuda.is_available()
False
```

TorchはCUDAが使えるGPUを認識していない

[https://zenn.dev/utahka/articles/ed881a568246f4](https://zenn.dev/utahka/articles/ed881a568246f4)
- > PyTorchのwheelファイルはCUDA込みなのでWSL内のUbuntuにCUDAとcudnnを入れる部分は実は不要ですよ。
- Windows に NVIDIA ドライバーをインストール
    - [https://developer.nvidia.com/cuda/wsl](https://developer.nvidia.com/cuda/wsl)

:

```
$ nvidia-smi
Fri Aug 26 22:32:57 2022
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 515.65.01    Driver Version: 516.94       CUDA Version: 11.7     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  On   | 00000000:01:00.0 Off |                  N/A |
| N/A   51C    P8    10W /  N/A |      0MiB /  8192MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|  No running processes found                                                 |
+-----------------------------------------------------------------------------+
```

`CUDA Version: 11.7`
- 11.5→11.7
- これはドライバーがサポートしている最大バージョンらしい

CUDA Toolkit
:

```
(ldm) nishio@DESKTOP-0ET2LJF:/mnt/c/WINDOWS/system32$ nvcc -V
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2019 NVIDIA Corporation
Built on Sun_Jul_28_19:07:16_PDT_2019
Cuda compilation tools, release 10.1, V10.1.243
```

TorchはCUDAが11.3であることを期待しているのに、実際には10.1?

WSL (Ubuntu) に CUDA Toolkit をインストール
- [https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&Distribution=WSL-Ubuntu&target_version=2.0&target_type=deb_local](https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&Distribution=WSL-Ubuntu&target_version=2.0&target_type=deb_local)
: 	

```
 wget https://developer.download.nvidia.com/compute/cuda/repos/wsl-ubuntu/x86_64/cuda-wsl-ubuntu.pin
 sudo mv cuda-wsl-ubuntu.pin /etc/apt/preferences.d/cuda-repository-pin-600
 wget https://developer.download.nvidia.com/compute/cuda/11.7.1/local_installers/cuda-repo-wsl-ubuntu-11-7-local_11.7.1-1_amd64.deb
 sudo dpkg -i cuda-repo-wsl-ubuntu-11-7-local_11.7.1-1_amd64.deb
 sudo cp /var/cuda-repo-wsl-ubuntu-11-7-local/cuda-*-keyring.gpg /usr/share/keyrings/
 sudo apt-get update
 sudo apt-get -y install cuda 
```


:

```
$ nvcc -V
...
Cuda compilation tools, release 10.1, V10.1.243
```

10.1のままだ

:

```
(ldm) $ sudo update-alternatives --config cuda
There is only one alternative in link group cuda (providing /usr/local/cuda): /usr/local/cuda-11.7
Nothing to configure.
conda install pytorch torchvision -c pytorch
```

えー、CUDAは11.7だけがインストールされてるってことになってるぞ？？
- 11.3をインストールする必要がある？
    - PyTorchは11.7で動くはずだという意見

:

```
(ldm) nishio@DESKTOP-0ET2LJF:~/stable-diffusion$ lspci
27fa:00:00.0 3D controller: Microsoft Corporation Device 008e
9e5b:00:00.0 3D controller: Microsoft Corporation Device 008e
```

lspciで見えないのはおかしい？
- lspciで見えないのはWSL環境ならそういうものらしい
    - [https://qiita.com/ksasaki/items/ee864abd74f95fea1efa](https://qiita.com/ksasaki/items/ee864abd74f95fea1efa)

:

```
$ sudo apt-get remove nvidia-cuda-toolkit
...
The following packages will be REMOVED:
  nvidia-cuda-toolkit
0 upgraded, 0 newly installed, 1 to remove and 2 not upgraded.
...

$ nvcc -V

Command 'nvcc' not found, but can be installed with:

sudo apt install nvidia-cuda-toolkit

$ sudo apt-get install cuda
Reading package lists... Done
Building dependency tree
Reading state information... Done
cuda is already the newest version (11.7.1-1).
```


うーん、nvccはnvidia-cuda-toolkitと紐づいていてバージョンは10.1
CUDA Toolkitの1.17をインストールしたのだがそちらになってくれない
両方アンインストールして、autoremoveして依存で入ったパッケージも全部消した上で、apt-get install cudaだけする

`Command 'nvcc' not found`になるなぁ

あ、パスが通ってないだけか
:

```
$ /usr/local/cuda/bin/nvcc -V
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2022 NVIDIA Corporation
Built on Wed_Jun__8_16:49:14_PDT_2022
Cuda compilation tools, release 11.7, V11.7.99
Build cuda_11.7.r11.7/compiler.31442593_0
```


condaの環境を消して作り直す
:

```
(ldm) $ python
>>> import torch
>>> torch.cuda.is_available()
True
```

やっとcuda availableになった！！

:

```
$ python scripts/txt2img.py --prompt "cat" --plms --ckpt sd-v1-4.ckpt
...
   attn = sim.softmax(dim=-1)
RuntimeError: CUDA error: unknown error
```

えええー

`$ python scripts/txt2img.py --prompt "cat" --plms --ckpt sd-v1-4.ckpt --n_samples 1 --W 256 --H 256`
- できた！

- [/motoso/Stable diffusionのimg2imgをGTX1070（VRAM 8GB）で使う#6307bc45774b170000b7fa8a](https://scrapbox.io/motoso/Stable diffusionのimg2imgをGTX1070（VRAM 8GB）で使う#6307bc45774b170000b7fa8a)
    - 半精度にするの意外と簡単そうだった
- できた！
    - exe版ではなくPythonスクリプトの側を実行して同じものを得られるようになった
    - ファイルから複数のプロンプトを投げた時にプロンプトごとにフォルダを作ってそれぞれをiter指定の枚数作成するようにした
        - 寝る前に「これとこれを50枚ずつ作っといてね」というやり方ができる
    - ついでにexe版と同じようにパラメータ情報の入ったJSONが出力されるようにした

- ファインチューニング試した情報
    - [https://birdmanikioishota.blog.fc2.com/blog-entry-8.html](https://birdmanikioishota.blog.fc2.com/blog-entry-8.html)
    - > 今回はcolabを利用し、画像16枚、学習は3時間程度でした。
        - 現実的に新しい概念を教えられそう

- [https://github.com/basujindal/stable-diffusion](https://github.com/basujindal/stable-diffusion)
    - forkしてGPUに分割して送るようにしたバージョン、VRAMが少なくても動くし、今動いてる人ももっと大きな画像を作れる、とのこと(まだ試してはない)


`$ python scripts/my.py --from-file prompts.txt --n_iter 100 --seed 130`
`$ python scripts/my.py --prompt "black cats" --n_iter 100 --seed 130`
