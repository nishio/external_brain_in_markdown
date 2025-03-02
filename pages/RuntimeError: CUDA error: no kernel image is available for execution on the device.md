

diffuserを試していた時に発生した。CUDAのバージョン違いではないかと確認したらその通りだった。

python

```
>>> import torch
>>> torch.__version__
'1.12.1+cu102'
>>> torch.version.cuda
'10.2'
```


Dockerfile

```
FROM nvcr.io/nvidia/cuda:11.7.1-cudnn8-runtime-ubuntu20.04
```


![image](https://gyazo.com/e732b22fc4c5681f219de25254bde4bf/thumb/1000)
[https://pytorch.org/get-started/locally/](https://pytorch.org/get-started/locally/)
`$ pip install --upgrade torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/cu113`

python

```
>>> torch.version.cuda
'11.3'
```

