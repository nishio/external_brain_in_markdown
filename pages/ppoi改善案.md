---
title: "ppoi改善案"
---

[[ppoi改善2021-02-05]]

2018-10-24
[[ppoi]]の改善案、使っている最中に直し始めると気が散るのでこちらにメモしておく

- unknown.txtをおいて欲しい旨がわからない
    - 具体的に何をするんかわからない
    - 書籍の裁断スキャンPDFをOCRしたデータ5冊分をcatした
    - `$ wc unknown.txt `
    - >  35203  110327 2069652 unknown.txt

python

```
>>> lines = open("unknown.txt").readlines()
>>> lines = [line for line in lines if line != "\n"]
>>> len(lines)
25762
>>> open("unknown.txt", "w").writelines(lines)
>>> from collections import Counter
>>> c = Counter()
>>>> for line in lines:
        c.update(line)
>>> c.most_common(100)
...
>>> len(c)
2851
>>> len([1 for k in c if c[k] > 9])
1513
>>> open("chars.txt", "w").write("".join([k for (k, v) in c.most_common() if v > 9]))
1513
```


- (将来の機能追加) initialize時に最低１つのpositiveとnegativeを入れろと言うが、別に入れなくても「両サイドのデータが入力されてなければ全部0.5」と判断して能動学習に進んだらいい
    - done in [[ppoi改善2021-02-05]]
- (検討) コマンドラインで実行されることを想定してるけど、ipython上で動くのでもよかったかもなぁ？
    - ipythonはinputを取れるのか？
- ppoi/unknown.txtをおけ、って伝わらないよね

今回OCR化けの判定なので
:

```
$ cat ppoi/positive.txt
|11111'「 11
$ cat ppoi/negative.txt
よ い取材をしな いと、 いくら器用 にそれをまとめたところで、 よ い判断 に到達する気づか い
```


user.pyのfeatureづくりを変更
python

```
CHARS = open("chars.txt").read()
def make_features(s):
    "take a string, return np.array"
    x = np.array([s.count(c) for c in CHARS], dtype=np.float)
    # normalize                                                                                                                            
    x =	x / x.sum()
    return x
```


能動学習の時に間違えて入力した場合のためにundoがあると良い
- 今はファイルを2つ開いて編集しなければならない

能動学習の最中に、クラスタを増やしたくなる
- 今回のケース、Yes/Noの他に「これじゃ短すぎて判断つかないよ」がある
