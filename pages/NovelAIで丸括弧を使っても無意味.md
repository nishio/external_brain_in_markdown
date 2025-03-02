---
title: "NovelAIで丸括弧を使っても無意味"
---

描画AIのプロンプトはサービスやシステムによって構文が違うのに、それを理解してない人がいる。
- たとえば丸括弧がたくさんついてるプロンプトをNovelAIに使っている人がいる。
- 丸括弧によるトークン強調はAUTOMATIC1111/stable-diffusion-webuiの機能、NovelAIでは機能しない。
- NovelAIでは中括弧を使う。ドキュメント: [Strengthening & Weakening Vectors - NovelAI Documentation](https://docs.novelai.net/image/strengthening-weakening.html)

プログラミングに例えると「ネットで見つけたJavaScriptのコードをコピーして、Pythonのコードにペーストする」ようなことをしている
- プログラミングではほとんどの場合エラーになるので「その行為は無益だ」と学ぶ機会になる
- 描画AIはプログラミングと違ってエラーが出ないから、おかしなプロンプトが再生産されてしまう

## 実証実験
model: NAI Curated, seed: 42, prompt: cat
![image](https://gyazo.com/76594a8a23249972f61bb4cfc3459330/thumb/1000)

このプロンプトの"cat"を20個の中括弧で$1.05^{20}$倍に強めるとこうなる
{{{{{{{{{{{{{{{{{{{{cat}}}}}}}}}}}}}}}}}}}}
![image](https://gyazo.com/80ea2782877cca9c0bd753493b0c897b/thumb/1000)
トークンを強めすぎてまともな絵の範囲から逸脱しているわけだ

一方で同じことを丸括弧でやるとこうなる
((((((((((((((((((((cat))))))))))))))))))))
![image](https://gyazo.com/ae3b0e5220ea114fa2c980ab8682a6c1/thumb/1000)
丸括弧は、トークンを強める構文として解釈されるのではなく、単なるプロンプトの文字列として解釈されている。
括弧はほとんど意味を持たないトークンなので、20個付いていてもあまり影響を与えることなく普通の猫の絵になっている。


from [/villagepump/2022/11/04](https://scrapbox.io/villagepump/2022/11/04)
- > [[元素法典]]は流出モデルで検証されているらしく()で描かれているのでこういうのの予感<img src='https://scrapbox.io/api/pages/villagepump/基素/icon' alt='/villagepump/基素.icon' height="19.5"/>

なるほどね、中国の人たちはNovelAIのサービスに接続できないのかな？当局に監視されてる？
流出モデルをAUTOMATIC1111/stable-diffusion-webuiに入れて使ってるのなら、プロンプトがそちらの構文になるのも納得だ。


[[NovelAIで丸括弧を使っても無意味(実験メモ)]]