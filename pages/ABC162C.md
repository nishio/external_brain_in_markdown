
> このCythonはTLE  [https://atcoder.jp/contests/abc162/submissions/11811351?lang=ja](https://atcoder.jp/contests/abc162/submissions/11811351?lang=ja)
> このPyPyは通る(947ms) [https://atcoder.jp/contests/abc162/submissions/11828688?lang=ja](https://atcoder.jp/contests/abc162/submissions/11828688?lang=ja)
> Cythonの使い方がよくないのかな？
[https://twitter.com/mec287117892/status/1249333553667555340](https://twitter.com/mec287117892/status/1249333553667555340)
PyPyはgcdの中身もJITコンパイルするが、Cythonは型宣言のついてないgcdを「オブジェクトを出し入れする関数だ」と判断してるのでintで宣言した変数を毎回オブジェクトに変換する

はい、[[Cython]]でAC 785 ms。PyPyより速い。
python

```
cdef gcd(int p, int q):
    cdef int r
    while q:
        r = p % q
        p = q
        q = r
    return p
 
 
def main():
    cdef int ans, i, j, l, K
    K = int(input())
    ans = 0
 
    for i in range(1, K+1):
        for j in range(1, K+1):
            for l in range(1, K+1):
                ans = ans + gcd(gcd(i, j), l)
    print(ans)
 
 
if __name__ == "__main__":
    main()
```

[https://atcoder.jp/contests/abc162/submissions/14918529](https://atcoder.jp/contests/abc162/submissions/14918529)

#atcoder
