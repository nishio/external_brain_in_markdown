---
title: "Ollama"
---

2024-04-26
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>ollamaとは何？英語で検索して日本語で解説して

<img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>Ollamaは、大規模言語モデル（LLM）をローカルで簡単に実行、作成、共有することを目的としたオープンソースアプリケーションです。このプラットフォームは、主にMacOSとLinuxで利用可能で、コマンドラインインターフェイスを通じて操作します。最初は[[Llama2]]モデルをサポートしていましたが、その後、[[Mistral]]や[[Phi-2]]などのモデルもサポートするようになりました​。
- (Isaac Chung)[What is Ollama? A shallow dive into running LLMs locally | Isaac Chung](https://isaac-chung.github.io/blog/what-is-ollama)​

Ollamaの特徴は、GPUがなくても大きなモデルを効率的に動かすことができる点です。これは、モデルの重みを量子化し、一部の層をCPU上で、他の層をGPU上で実行することにより、効率的な推論を実現しています。このため、大規模モデルでもローカルの限られたリソース内で動作可能です​​。
- (Mitja Martini)[Ollama on Windows: How to Install and Use it with OpenWebUI | Mitja Martini](https://mitjamartini.com/posts/ollama-on-windows/)

Ollamaを使用する主な理由は、大規模な言語モデルを第三者のクラウドサーバーに依存せずに自分のハードウェア上で安全に実行できることにあります。これにより、ユーザーデータのプライバシーを保護しつつ、必要に応じて独自のカスタマイズや拡張が可能です。また、モデルのダウンロードから管理、実行までを簡単に行うことができ、さまざまなモデルを試すことも容易になります​​。
- (GitHub) [ollama/ollama: Get up and running with Llama 3, Mistral, Gemma, and other large language models.](https://github.com/ollama/ollama)
- (Isaac Chung)

総じて、Ollamaはプログラミングスキルがあるユーザーや、第三者のサービスを使用せずに言語モデルを自分の環境で動かしたいと考えている人々に適しています。


> [_saip_](https://twitter.com/_saip_/status/1783309599480668508) Ollama、インストールして
>  $ ollama run phi3
>  で即[[Phi-3]]が使えるの、体験がすごい！
>  初回はpullする必要があるけど2回目以降は速攻使えて、モデルロードとかないんか…？となった。
> [_saip_](https://twitter.com/_saip_/status/1783310216827990465) VRAM8GBのローカル環境で、引くほど早く日本語生成してた。文章は支離滅裂だったけど、Instruction Tuningされてる気配がしたのでちゃんとInstruction書いてあげればいい感じに動くのでは？と思った。
