
from [[ARC114]]
ARC114C🤔
- 考えたこと
    - ![image](https://gyazo.com/abf29c4b3ac48a4522111516f8694de1/thumb/1000)
    - ![image](https://gyazo.com/e7f8cd4610488b139ec0cce79f6b875d/thumb/1000)

- > C問題は、1回目の操作では全体にv=min(A)として操作するのがいいね。そうするとmin(A)の場所ごとに分割して同じ問題を解けばよくなるよ。あとは分割のされ方に注目すると、もとの問題の答えをf(N,M)として、「全てのl,r,kに対しての、(1回目の操作をv=kに対して、区間[l,r)が残るようなAの個数)×f(r-l,M-k)」の和が求まれば良くて、そのままだとO(N^2 M^2)だけど、累積和を使うとO(NM)になるよ [tw](https://twitter.com/kyopro_friends/status/1371104057004150784)
