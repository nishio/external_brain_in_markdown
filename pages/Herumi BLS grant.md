---
title: "Herumi BLS grant"
---

[https://blog.ethereum.org/2019/11/08/eth2-quick-update-no-3](https://blog.ethereum.org/2019/11/08/eth2-quick-update-no-3)
> Herumi BLS grant
>  We've given out a grant to Shigeo Mitsunari, the maintainer of the super-fast Herumi pairing library and BLS signature library. This grant is to bring the libraries up to spec with the new BLS standard (new hash-to-G2, constant-time signing, etc) as well as to help accomplish some more practical items for eth2 usability (Rust integration, fuzzing work, etc).
>  In addition to the feature component of the grant, there is also a performance component. The Herumi library is already 2-3x faster than the next best BLS option, but because signature verification is one of the main bottlenecks in eth2, any additional gains here would be excellent, enabling eth2 to run under even higher load and in more adverse scenarios. Shigeo will spend some additional time and effort further optimizing the library to ensure it runs as fast as possible 🚀.
<img src='https://scrapbox.io/api/pages/nishio/o1 Pro/icon' alt='o1 Pro.icon' height="19.5"/>
### 解説（初心者向け）
- [[Ethereum 2.0]] では、多数のバリデータが出す「[[BLSシグネチャ]]」（[[デジタル署名]]の一種）の検証が非常に重要です。これらの署名を大量かつ素早く確認できるかどうかが、ネットワーク全体のパフォーマンスに大きく影響します。

### Herumiライブラリとは？
- 開発者の[[光成 滋生]] ([[Shigeo Mitsunari]]) 氏が作っている、[[BLS署名]]を高速に処理できるライブラリです。
- 他のBLS実装と比べて 2～3倍ほど速いとされています。
- [[Ethereum Foundation]] はこのライブラリが新しいBLS標準（新しいアルゴリズム仕様やセキュリティ強化）に対応できるよう助成金（グラント）を提供。
- Rustへの統合やファジングテスト（バグ検出の一手法）など、使いやすさと安全性向上のための作業も支援しています。

つまり、### Ethereum 2.0 が大量の署名検証を効率的にこなすため、Herumiの高速BLS実装は不可欠
であり、開発者への支援を通じてパフォーマンスやセキュリティ強化が図られているのです。


[[eth2]]
[[光成 滋生]] / [[herumi]]
