
[B - Flip Digits](https://atcoder.jp/contests/agc049/tasks/agc049_b)
![image](https://gyazo.com/9ba0804fe68f50c3755d1445acfb90cb/thumb/1000)

from [[AGC049]]
AGC049B
- 考えたこと
    - 行われる操作は01→10か11→00かのどちらか
    - 後ろから考える
        - ![image](https://gyazo.com/cf7f0cc4abb2a7ed8bb21c47b8a9a937/thumb/1000)
        - ケース1の時、末尾の1どうしはベアになる
            - 消えることができないから
        - ケース2の時、消して良いのか？
        - 削除可能回数でDP？
            - N=10^5だから10^4くらい削除可能な時に辛い
        - ケース2の時、消して良いのか？→よくない
            - S: 110011
            - T: 001100
            - この時後ろを先に消してしまうと達成不能になる
            - 前からやる？
    - 前からやる
        - ![image](https://gyazo.com/df77fbc848e01430899c56bdbd3d99ff/thumb/1000)
        - [[貪欲法の証明パターン]]
        - 削除するパターンが最適解の中にあるとすると、削除する場所を交換してよりよい解が作れるので、最適解であるという前提に矛盾する、よって削除するパターンはない
        - AC

    - Tweet:
        - 操作は1を一つ左に動かすか、2個を消すか。
        - 最も左の1に注目しSの方が左である時、解があるとするならその1は消えなければならないので消すのにかかるコストを回答に足して、注目する1を2つ先のものにする。
        - 逆の場合は先頭の1を消しても損であることから最適解では消されない。
            - Sの先頭の1をTの先頭の1まで動かすコストを回答に足して、それぞれ次の1に注目する。
        - 最後までたどり着いたらそれは最適解なので回答を返す。
        - Sが足りなくなるなどの不整合が起きたら、解が存在しないとわかる。
        - 僕の実装では先に1が立っている場所を列挙しているけど、これはやらなくても解けるかもしれない。
            - 「次の1に注目」が添え字のインクリメントになるのでコードはわかりやすい。
python

```
def solve(N, S, T):
    spos = []
    tpos = []
    diff = 0
    for i in range(N):
        if S[i] == 1:
            spos.append(i)
            diff += 1
        if T[i] == 1:
            tpos.append(i)
            diff -= 1

    if diff % 2 == 1:
        return -1
    if diff < 0:
        return -1

    tpos += [N] * N
    spos.append(-1)
    i = 0
    j = 0
    ret = 0
    while i < len(spos) - 1:
        if spos[i] < tpos[j]:
            # spos_i should be deleted
            next = spos[i + 1]
            if next == -1:
                return -1
            ret += (next - spos[i])
            i += 2
            continue

        ret += (spos[i] - tpos[j])
        i += 1
        j += 1
    if j != len(tpos) - N:
        return -1
    return ret
```

