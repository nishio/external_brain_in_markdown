---
title: "Qwen 3.6"
---

[[Local LLM]]実験

2026-08-18
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> Qwen 3.6 27Bのコンテキストサイズは？
<img src='https://scrapbox.io/api/pages/nishio/Codex/icon' alt='Codex.icon' height="19.5"/>モデル自体の最大コンテキストは262,144トークンです。
ただし現在のOpenCode設定は、RTX 5080 16GBで安定動作させるため16,384トークンに制限しています。最大出力は8,192トークンで、system prompt・履歴・入力・出力をすべて16K内に収めます。
27Bモデル本体だけで約16.35GBあるため、32K以上にするとCPU offload増加や大幅な低速化が予想されます。

---
16Kではあっという間に使い切ってcompactionが走ってしまうな〜

---
9Bなら64Kで問題なく動く
> VRAM：約6.63GB

---
9Bだと言語の一貫性がイマイチだからWikiをこねるとかにはイマイチむかなさそうだなぁ

