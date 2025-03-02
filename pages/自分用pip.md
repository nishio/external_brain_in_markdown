---
title: "自分用pip"
---

PyPIに登録するほど気合は入ってないが、複数のプロジェクトで使いたくなったコード片を、pipでインストールできるようにしてGithubに置く。
バージョンを固定したり最新にしたりはpip自体の機能でできるので考えることが減る。

- setup.pyを書く
    - 公式の最小限の解説
    - [Minimal Structure — Python Packaging Tutorial](https://python-packaging.readthedocs.io/en/latest/minimal.html)
- まずはローカルのファイルシステムでpip installできることを確認する
    - `$ pip install .`
- Githubにpushする
- Githubからpip installできることを確認する
    - `$ pip install git+https://github.com/nishio/rich_tokenizer`


- これだとpip freezeした時にgitからinstallしたって情報が失われてそう
    - `$ pip install git+https://github.com/nishio/rich_tokenizer`
- これが良さそう
    - `$ pip install -e git+https://github.com/nishio/rich_tokenizer#egg=rich_tokenizer`
- これならpip freezeに`-e git+https://github.com/nishio/rich_tokenizer@4284...af7e#egg=rich_tokenizer`と出力される
- [python - How to state in requirements.txt a direct github source - Stack Overflow](https://stackoverflow.com/questions/16584552/how-to-state-in-requirements-txt-a-direct-github-source)

参考
- [python - pip install from git repo branch - Stack Overflow](https://stackoverflow.com/questions/20101834/pip-install-from-git-repo-branch)
    - [Pythonで作ったコマンドをGitHub経由でpipインストール可能にする | Developers.IO](https://dev.classmethod.jp/articles/pip-install-via-github-command/)
    - [https://github.com/pallets/flask](https://github.com/pallets/flask) がサンプルとしてよい
    - [navdeep-G/setup.py: 📦 A Human's Ultimate Guide to setup.py.](https://github.com/navdeep-G/setup.py)
    - [Minimal Structure — Python Packaging Tutorial](https://python-packaging.readthedocs.io/en/latest/minimal.html)