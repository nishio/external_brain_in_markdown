---
title: "Random Kitchen Sinks"
---

[[Random Features for Large-Scale Kernel Machines]]（Rahimi & Recht, NIPS 2007）
- カーネルをランダム特徴（例: ランダムフーリエ特徴）で近似し、線形学習で高速化。
- [PDF](https://papers.nips.cc/paper_files/paper/2007/file/013a006f03dbc5392effeb8f18fda755-Paper.pdf)
- 続編 [[Weighted Sums of Random Kitchen Sinks: Replacing Minimization with Randomization in Learning]]（Rahimi & Recht, NIPS 2008/Proc. 2009）
    - 「RKS」を一般化し、ランダム非線形基底の重み付け和として解析。


<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>
なにを近似するの？
- 本来のGP（[[ガウス過程回帰]]）は[[カーネル]] (k(x,x')) を使って近い点は近い予測になる、という滑らかさを表現します。
- しかし厳密GPは O(N³)（N=学習点数）で重い。
- そこでランダム特徴（[[Random Fourier Features]]; [[RFF]]）で「カーネル ≒ 内積」になる明示的な特徴マップ ($\phi(x)$) を作り、その上で[[線形回帰]]（≒[[ベイズ線形回帰]]）をします。
- これが「ランダム特徴×線形回帰」によるGP近似です。
- 別名 Random Kitchen Sinks。

直感（なぜ効くの？）
- [[RBF]]系カーネルはフーリエ変換で表せる →ランダムな波（周波数・位相）を足し合わせると、“なめらかな”関数空間を近似できる。
- だから「$\phi(x)$ = ランダム波のベクトル」に変換して、($\hat y = w^\top \phi(x)$) を学習すれば、非線形回帰を線形回帰で置き換えられる。

数式（最小セット）

1) ランダム特徴（RBFカーネルの例）
- RBF: $k(x,x') = \exp(-|x-x'|^2 / (2\ell^2))$
- ランダムに $\omega_j \sim \mathcal{N}(0,\frac{1}{\ell^2}I)), (b_j \sim \mathrm{Unif}[0,2\pi]$
- 特徴写像（次元 D）
- $\phi_j(x) = \sqrt{\frac{2}{D}} \cos(\omega_j^\top x + b_j), \quad j=1,\dots,D$
- すると $k(x,x') \approx \phi(x)^\top \phi(x')$

埋め込みが**正規化済み（L2=1）**なら、ユークリッド距離の代わりに
コサイン距離 ($1 - x\cdot x'$) を使うRBF相当も実務上OK。
実装は「ランダム射影→cos」を踏むだけで十分です。

2) 線形回帰（ベイズ版＝不確実性も出せる）
- 観測：($y = \Phi w + \varepsilon), (\varepsilon \sim \mathcal{N}(0,\sigma_n^2 I)$)
ここで $\Phi$ は $[\phi(x_1)^\top; \dots; \phi(x_N)^\top]$
- 事前：$w \sim \mathcal{N}(0,\lambda^{-1} I)$（ridge正則化）
- 事後平均・分散：
    - $\Sigma = \big(\lambda I + \tfrac{1}{\sigma_n^2}\Phi^\top \Phi \big)^{-1},\qquad \mu_w = \tfrac{1}{\sigma_n^2}\Sigma \Phi^\top y$

- 予測平均・分散（新点 (x_*)）：
    - $\mu(x_*) = \phi(x_*)^\top \mu_w,\quad \mathrm{Var}(x_*) \approx \phi(x_*)^\top \Sigma, \phi(x_*) + \sigma_n^2$
- UCB は $\text{UCB}(x)=\mu(x)+\sqrt{\beta}\sigma(x)$
ここまでで**GPらしい「平均＋不確実性」**が低コストで手に入る。

手順（実装フロー）
1. 前処理
    - 文章→埋め込み（例：1536次元）
    - L2正規化（重要：コサインを距離に使いやすい）
2. RFFの準備（1回だけ）
    - 次元 D を決める（MVPなら 256〜1024）
    - 乱数 (\omega, b) を固定（seed保持／毎回再生成しない）
3. 学習セット作成
    - 評価済みの ((x_i, y_i)) から (\Phi) を作る
    - (\Sigma, \mu_w) を計算（D×Dの行列を1回だけ逆行列）
4. 未評価点の推論
    - 各 (x) に φ(x) を当てて (\mu(x), \sigma(x)) を求める
    - UCB順に並べ、MMRで多様性を確保して提示
5. 新しい評価が貯まったら再学習（軽い）

パラメータの目安
- D（RFF次元）：256（超軽量）〜1024（精度↑、コスト↑）
- (\ell)（長さスケール）：0.5〜1.0 相当（埋め込みの距離感に依存）
- (\lambda)（事前精度・ridge）：1.0 前後から。過学習で上げる
- (\sigma_n)（観測ノイズ）：0.2 前後（評価のブレ対策。重複評価から推定可）
- (\beta)（UCBの探索度）：1.0〜2.0（大きいほど探索寄り）

どこが「軽い」の？
- ボトルネックは D×D の逆行列（一回）で、O(D³)。
D=512 なら JS/Deno でも数百 ms〜数秒で収まる規模。
- その後の推論は各点 O(D)（速い）。
- 厳密GPの O(N³) と比べて段違いに軽量。

よくある落とし穴
- RFFを毎回再生成してしまう → 学習と推論でφが一致せず崩壊。
→ 乱数は固定（seed管理）。
- 埋め込みを正規化しない → 距離スケールが壊れてσが変。
→ L2=1を徹底。
- Dが小さすぎ → バイアス（表現力不足）。
→ 256→512→1024…と上げて検証。
- 数値不安定 → (\lambda) を少し上げる／二重精度／小さなεで発散防止。
- UCBが似た候補ばかり → MMRで多様性ペナルティ（既選択とのコサイン最大値を減点）。

極小の疑似コード（TypeScript/Edge Functions風）
ts

```typescript
// 準備（1回）: RFFパラメータ
const D = 512, l = 0.7;            // 次元と長さスケール
const W = randn(d, D, 1/(l*l));    // N(0, 1/l^2)
const b = uniform(D, 0, 2*Math.PI);

const phi = (x: number[]) => {
  const u = l2norm1(x);            // L2正規化
  const z = new Array(D);
  for (let j=0;j<D;j++){
    let s = 0; for (let i=0;i<d;i++) s += W[i][j]*u[i];
    z[j] = Math.SQRT2*Math.cos(s + b[j])/Math.sqrt(D);
  }
  return z;
};

// 学習（評価が貯まるたび）
const Phi = X_labeled.map(phi);    // N×D
const XtX = gram(Phi);             // D×D
const A   = addDiag(XtX, lambda);  // ridge
const Ainv= inv(A);
const Xty = Phi[0].map((_,j)=> dotCol(Phi,j, y)); // D×1
const w   = matvec(Ainv, Xty);

// 予測（未評価）
for (const x of X_unlabeled) {
  const p  = phi(x);
  const mu = dot(w, p);
  const var= quad(p, Ainv) + sigma_n*sigma_n;
  const ucb= mu + Math.sqrt(beta)*Math.sqrt(var);
  // → ucb順 + MMR で提示
}
```


まとめ
- RFF×線形回帰は、GPの“平均と不確実性”を軽量に再現する実用近似。
- Edge Functions（Deno/TS）でも回るので低コストMVPに最適。
    - 500件ならEdge Functionsでいけたが、1000件だとタイムアウトになる<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
- まずは D=256–512、L2正規化、乱数固定、UCB係数=1.5 で十分。
- 物足りなくなったら D↑ または **Pythonワーカー（GPyTorch）**へ移行。
