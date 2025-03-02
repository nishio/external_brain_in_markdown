---
title: "LLMプロダクト開発者がMac Studioを買ってローカルLLMを触るべき理由"
---

[LLMプロダクト開発者がMac Studioを買ってローカルLLMを触るべき理由｜erukiti](https://note.com/erukiti/n/n58a8180ea9fb)
[[LLMプロダクト開発者]]が[[Mac Studio]]を買って[[ローカルLLM]]を触るべき理由
<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>
LLMプロダクト開発において、ローカルLLMを無視できない状況になってきた。ローカルマシンでLLMを高速検証するために、メモリを大量に積んだ[[Mac Studio]]が良い選択肢になる。

主な理由は以下の通り:
1. 最先端のLLMはもはやGPT-4ではなく、Claude3 OpusやHaikuなどが優れている。
2. Apple Siliconの[[UMA]]により、メモリの大半をGPUメモリに割り当てられ、大規模LLMを動かせる。
3. 今年になって[[Command-R+]]や[[Llama3:70b]]など、実用レベルのローカルLLMが登場した。
4. LLMのAPIコストは高額だが、ローカル実行ならコストを無視できる。
5. 大規模LLM検証にはGPUメモリ64GB以上が望ましいが、NVIDIAの場合セットアップが大変。一方Mac Studioは手軽。
6. LLMプロダクト開発では膨大な実験が必要で、会社がマシンを提供するのが望ましい。

NVIDIAマシンも良い選択肢だが、手軽さと安価さではMac Studioが秀でている。最先端のLLMプロダクト開発競争に乗り遅れないためにも、Mac StudioでローカルLLMを触ることが推奨される。

> [mutaguchi](https://twitter.com/mutaguchi/status/1783271081681580482)
>  「LLMプロダクト開発者がMac Studioを買ってローカルLLMを触るべき理由」の記事のはてブコメント見てたんだけど、ほとんど理解されてなかったのが興味深い。...
<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>
以下のように要約できます。
1. ローカルLLMの実用性が高まってきた背景として、プロプライエタリなLLMのランニングコスト、機微情報の流出問題、BAN問題などがある。
2. ローカルLLMプロダクト開発では推論性能が重要で、そのためにはVRAMレベルの高速メモリが必要。現状ではMac Studioが最適。
3. 一般家庭レベルの機器でローカルLLMが動作する日は近いが、開発者は今すぐMac Studioを使った検証・開発を進めるべき。クラウドよりコストが安い。
4. ローカルLLMプロダクトは売り物になりにくく、自社利用のために開発するケースが多いだろう。
5. 商用LLMとローカルLLMでは設計が大きく異なる。ローカルLLMは気軽に呼び出せるAPIのように使える。

つまり、ローカルLLMの実用性向上を受けて、開発者はいち早くMac Studioを活用した検証・開発を進めるべきだが、それは自社利用が主な目的になると考えられる、ということですね。