---
title: "PTX"
---

<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>
[[DeepSeek]]では、[[CUDA]]の代わりに、NVIDIAが提供するPTX（[[Parallel Thread Execution]]）という中間言語を用いています。
PTXは、CUDA C/C++のコードから生成される[[低水準]]の[[中間表現]]で、GPUの[[機械語]]に近い形で最適化が可能となるため、より細かなハードウェア制御が実現できます。
