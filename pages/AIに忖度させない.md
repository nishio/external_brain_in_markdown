---
title: "AIに忖度させない"
---

> ![image](https://pbs.twimg.com/media/G8THomva4AIqAlZ?format=jpg&name=medium#.png)
> [nishio](https://x.com/nishio/status/2000935611109367882) この聞き方はLLMの忖度を誘発するからあんまり良くなさそう
>  >ainsophyao: LLM 悪口がひどい。
>  > この文章は、「教科書の定義をいくつかコピペレベルで知っているが、それらの論理的な整合性を理解できておらず、数式の意味も誤解している人物」が、マウントを取るために無理やり難解な言い回しを使っている、典型的な「似非（えせ）科学的解説」です。

> [sonson_twit](https://x.com/sonson_twit/status/2000941292587770068) 忖度を防ぐ会話の方法ってあるんですか・・・・。知りたいです・・・。

> [nishio](https://x.com/nishio/status/2000942998985826385)
>  1: リンクで渡すとreplyもコンテキストに入るので本文だけにする
>  2: 良い悪いの価値判断をLLMに与えないで単に「解説して」と言う
>  3: その結果としてLLMは理解しようとし「言い過ぎや式に誤植があるけど〜という意図なんじゃないか」と好意的に歩み寄ろうとした上で元文章の誤りを指摘する
>  ![image](https://pbs.twimg.com/media/G8TGEKVaMAEUJ4r?format=png&name=small#.png) ![image](https://pbs.twimg.com/media/G8TGbmgboAAejWc?format=png&name=small#.png) ![image](https://pbs.twimg.com/media/G8TGzara4Agz5pD?format=png&name=small#.png) ![image](https://pbs.twimg.com/media/G8THB5Fa0AAJD-E?format=png&name=small#.png)

> [nishio](https://x.com/nishio/status/2000944318056685831) 念の為、僕が何に対して「よくない聞き方だ」と言ったかもスクショしておきます。改めてこれをみると
>  - 文章の質が悪い趣旨の価値判断をLMMに伝えている
>  - その上で「詳細に分析せよ」と言っている
>  ので、「これは質の悪い文章である、分析せよ」という趣旨のプロンプトになってしまっている。「分析」が何を指すのかは明瞭ではないが、「悪い」という価値判断はgivenなので、その前提の上での作文が行われる。
>  ![image](https://pbs.twimg.com/media/G8THomva4AIqAlZ?format=jpg&name=medium#.png)

> [sonson_twit](https://x.com/sonson_twit/status/2000944884971397335) なるほど。

> [nishio](https://x.com/nishio/status/2000945602956517394) あとはまあ、どぎつい酷評が出てきたのは、この「悪い」とプロンプトした文章へのreplyに似たような趣旨の批判が含まれているのも影響してるかもですね。
>  「悪い」とプロンプトしたものへの批判的replyなのでLLMが有用なものと思ってしまっている。

> [sonson_twit](https://x.com/sonson_twit/status/2000945982620725493) なるほど・・・勉強になります
>  いつも、思った感じで議論すると、なんか迎合してくるのが嫌で話の持って行き方に苦労してました
>  ありがとうごさいます

> [nishio](https://x.com/nishio/status/2000947700905447639) 自分の文章に対してはChatGPTの一時チャットを使って記憶を飛ばした上で「[[ファクトチェック]]して」「[[批判的に分析]]して」「ちょっとこの文章わかりにくいんだけどどういうこと」などとニュートラル〜ネガティブなプロンプトをしています

