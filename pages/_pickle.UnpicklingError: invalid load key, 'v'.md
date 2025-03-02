
> git lfsが入ってない場合、事前学習済みのモデルのクローンで実体の代わりにポインタ情報が取れてきてしまうので、コードを実行したときに_pickle.UnpicklingError: invalid load key, 'v'.みたいなことを言われてしばらくハマりました。
[https://zenn.dev/ryoma310/articles/63bc3d20a8746c](https://zenn.dev/ryoma310/articles/63bc3d20a8746c)

[[Textual Inversion]]の環境構築で、[[Stable Diffusion]]の4ギガあるモデルファイルをコピーして配置したが、おそらくこのモデルの中から別のモデルを参照しており、それが見つからないことが原因でこのエラーになった

`$ apt-get install git-lfs`
`$ git lfs install`
`$ git lfs pull`
