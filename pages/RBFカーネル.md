---
title: "RBFカーネル"
---

これ歴史的経緯で名前の指す概念がブレてるから初見の人には親切でないよね
- [[RBF]] = [[Radial basis function]]
    - [Radial basis function - Wikipedia](https://en.wikipedia.org/wiki/Radial_basis_function)
        - [放射基底関数 - Wikipedia](https://ja.wikipedia.org/wiki/%E6%94%BE%E5%B0%84%E5%9F%BA%E5%BA%95%E9%96%A2%E6%95%B0)
        - これ自体は「距離によってのみ決まる関数(radial function)」を基底関数(basis function)にするという抽象度の言葉
        - その「距離によってのみ決まる関数」の具体例としてガウス関数を使うことがメジャー
- この「ガウス関数を基底関数に使うこと」自体をRBFと呼ぶこともしばしばある
    - これは概念の抽象度がブレてると思う
    - [RBF — scikit-learn 1.7.2 documentation](https://scikit-learn.org/stable/modules/generated/sklearn.gaussian_process.kernels.RBF.html)
    - [[ガウシアンカーネル]]

<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>
要約：あなたの説明は概ね正しいです。特に「RBF＝距離だけに依存する関数を基底に使う発想」「ガウス関数が代表例」は事実です。ただし実務では “RBFカーネル＝ガウスカーネル=squared exponential kernel” を指す用法が定着しており、ここが混乱点です。
- RBFの広い意味（数学・補間・RBFネット）：RBFは「中心からの距離にのみ依存する関数」を基底として使う考え方。ガウスや多重二次、薄板スプラインなどが例。([ウィキペディア](https://en.wikipedia.org/wiki/Radial_basis_function?utm_source=chatgpt.com))
- “RBFカーネル”の狭い実務用法：機械学習（SVM/GPR）では RBF＝squared exponential kernel＝ガウス として実装・表記されることが多い（scikit-learnの`RBF`や`rbf_kernel`がそのままガウス）。([scikit-learn.org](https://scikit-learn.org/stable/modules/generated/sklearn.gaussian_process.kernels.RBF.html?utm_source=chatgpt.com))
- 教科書でも用語ゆれの明示：GPの標準的文献（Rasmussen & Williams）は「この共分散関数はRBFやGaussianとも呼ばれるが、ここではsquared exponentialと呼ぶ」とはっきり書いており、用語のブレが歴史的に存在。([the Gaussian Process web site](https://gaussianprocess.org/gpml/chapters/RW.pdf))
- 研究論文でも同義扱い：「Gaussian RBF（＝[[square-exponential]]/[[exponentiated-quadratic]]）」と同義で記述される例が一般的。([arXiv](https://arxiv.org/pdf/1807.02582?utm_source=chatgpt.com))

結論（ファクトチェック）
- 「RBF＝Radial Basis Function」→ 正しい。([ウィキペディア](https://en.wikipedia.org/wiki/Radial_basis_function?utm_source=chatgpt.com))
- 「“距離のみ”に依存する関数を基底にする概念」→ 正しい。([ウィキペディア](https://en.wikipedia.org/wiki/Radial_basis_function?utm_source=chatgpt.com))
- 「ガウス関数がメジャーな具体例」→ 正しい。([ウィキペディア](https://en.wikipedia.org/wiki/Radial_basis_function))
- 「“RBF”が“ガウス（SE）カーネル”そのものを指す用法がしばしばある」→ 正しい（実装・教科書・論文で確認）。([scikit-learn.org](https://scikit-learn.org/stable/modules/generated/sklearn.gaussian_process.kernels.RBF.html?utm_source=chatgpt.com))

実務での言い換え提案
- 広い意味を指すときは “radial（等方）カーネル”、狭い意味（ガウス）を指すときは “SE（=Gaussian/RBF）カーネル” と明記すると、初学者にも親切です。([cs.cornell.edu](https://www.cs.cornell.edu/~bindel/class/sjtu-summer18/lec/2018-06-27.pdf?utm_source=chatgpt.com))


[[Gaussianカーネル]]
[[ガウシアンカーネル]]
[[ガウスカーネル]]
[[Squared Exponential kernel]]
- SEカーネル: この表記は日本語でみたことはないなぁ
