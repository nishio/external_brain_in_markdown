
[B - 天下一リテラル](https://atcoder.jp/contests/tenka1-2015-qualb/tasks/tenka1_2015_qualB_b)
- Pythonのサブセット的な言語をパースして辞書リテラルか集合リテラルか区別する問題
- 一瞬「どこまで真面目に実装すべきか？」と迷う
    - 空辞書を除外すれば入力の2文字目以降に一つリテラルがあるのは確定
    - それを読み飛ばして、次の文字がカンマかコロンかで識別できる
- 真面目にプログラミング言語を実装する用途ならこの「読み飛ばし」の部分で真面目にリテラルをパースする
    - 今回は読み飛ばせればOK
    - 集合リテラルも辞書リテラルもカッコがバランスしてるからバランスするところまで読み飛ばすだけでいい
python

```
def parse(s, i):
    if s[i] in string.digits:
        while s[i] in string.digits:
            i += 1
    else:
        bracket = 1
        i += 1
        while bracket:
            if s[i] == "{":
                bracket += 1
            elif s[i] == "}":
                bracket -= 1
            i += 1
    if s[i] == ":":
        return "dict"
    else:
        return "set"


def solve(s):
    if s == "{}":
        return "dict"
    assert s[0] == "{"
    return parse(s, 1)
```


