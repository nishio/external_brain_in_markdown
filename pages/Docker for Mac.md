---
title: "Docker for Mac"
---

MacでChainerを使うのはサポートされてないし、なんか作った後サーバで動かそうと思ったときに移植の手間があるの面倒だからDockerでやることにした

`$ brew install docker`
`$ brew cask install docker`
`$ docker run -p 8888:8888 --name ml -it asashiho/ml-jupyter-python3`
- [機械学習を勉強するときはDockerを使うと便利 - あさのひとりごと](http://dr-asa.hatenablog.com/entry/2017/08/21/185301)
- [https://hub.docker.com/r/asashiho/ml-jupyter-python3/~/dockerfile/](https://hub.docker.com/r/asashiho/ml-jupyter-python3/~/dockerfile/)
- 実行するとJupyter Notebookが起動する
- Ctrl-Cした後、コンテナは消えていないが、stopしている状態になる
    - `$ docker start /ml`
    - `$ docker exec /ml pwd`
    - /notebooks

データファイルや結果ファイルなどを外からアクセスしたければVolumesではなくBind mountsが良さそう
- [https://docs.docker.com/storage/#choose-the-right-type-of-mount](https://docs.docker.com/storage/#choose-the-right-type-of-mount)

`$ docker run -p 8888:8888 --name ml -it --mount type=bind,source=/Users/nishio,target=/notebooks/home asashiho/ml-jupyter-python3`

メモ
- Chainerが入っていない
- pipは古い
    - You should consider upgrading via the 'pip install --upgrade pip' command.
    - # pip install --upgrade pip
- 3割くらい遅くなっちゃうなぁ
