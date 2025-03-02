
from [[AtCoder Library Practice Contest]]
ACLPC_F
[F - Convolution](https://atcoder.jp/contests/practice2/tasks/practice2_f)
- ![image](https://gyazo.com/dde1796c658447207ea2ef7a288c65a8/thumb/1000)
- 素朴に[[畳み込み]]をするとO(NM)
- [[FFT]]で使われる[[バタフライ演算]]を応用するとO(N logM)
    - [https://www.onosokki.co.jp/HP-WK/eMM_back/emm140.pdf](https://www.onosokki.co.jp/HP-WK/eMM_back/emm140.pdf)
- [[NTT]]という選択肢もあるらしい
