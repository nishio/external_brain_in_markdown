---
title: "Herumi BLS grant"
---

[https://blog.ethereum.org/2019/11/08/eth2-quick-update-no-3](https://blog.ethereum.org/2019/11/08/eth2-quick-update-no-3)
> Herumi BLS grant
>  We've given out a grant to Shigeo Mitsunari, the maintainer of the super-fast Herumi pairing library and BLS signature library. This grant is to bring the libraries up to spec with the new BLS standard (new hash-to-G2, constant-time signing, etc) as well as to help accomplish some more practical items for eth2 usability (Rust integration, fuzzing work, etc).
>  In addition to the feature component of the grant, there is also a performance component. The Herumi library is already 2-3x faster than the next best BLS option, but because signature verification is one of the main bottlenecks in eth2, any additional gains here would be excellent, enabling eth2 to run under even higher load and in more adverse scenarios. Shigeo will spend some additional time and effort further optimizing the library to ensure it runs as fast as possible 🚀.

[[eth2]]
[[光成 滋生]] / [[herumi]]
