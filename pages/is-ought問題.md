---
title: "is-ought問題"
---

<img src='https://scrapbox.io/api/pages/nishio/Claude/icon' alt='Claude.icon' height="19.5"/>
- 「〜である」（[[事実]]）をいくら積み重ねても、それだけからは「〜すべきだ」（[[規範]]）は論理的に出てこない、という問題
    - [[ヒュームの法則]]、[[ヒュームのギロチン]]とも呼ばれる
    - 事実と規範のあいだに線を引いてしまうのでギロチン

出典
- [[デイヴィッド・ヒューム]]『[[人間本性論]]』（1739-40）第3巻 第1部 第1節
- > In every system of morality, which I have hitherto met with, I have always remark'd, that the author proceeds for some time in the ordinary way of reasoning ... when of a sudden I am surpriz'd to find, that instead of the usual copulations of propositions, is, and is not, I meet with no proposition that is not connected with an ought, or an ought not.
- 意訳: これまで見てきた道徳の体系では、著者はしばらく普通に「である」「でない」で論じているのに、いつの間にか「べきである」「べきでない」の文ばかりになっている
    - この移行は新しい関係を言っているのだから、それがどうして全く別の関係から導けるのか、理由を示すべきだ、とヒュームは言う

例
- 「この薬は痛みを和らげる」（事実）→「この薬を飲むべきだ」（規範）
    - 間に「痛みは和らげるべきだ」という規範の前提が隠れている
    - 隠れた規範の前提を足せば論理的には通る。問題は、その規範の前提自体はどこから来るのか
- 「人間は昔からこうしてきた」→「だからこうすべきだ」
    - [[進化心理学]]の知見を規範に読み替える時によく起きる飛躍

よく混同されるもの
- [[自然主義的誤謬]]（[[G.E.ムーア]]『[[倫理学原理]]』1903）
    - 「善」を「快い」「進化的に有利」など自然的な性質で定義しようとする誤り、という主張
    - 「である」から「べき」への飛躍の意味で使われることが多いが、元々は「善の定義」についての議論で、ヒュームの問題とは別物

反論・解釈
- ヒューム自身は「導けない」と言い切ったのか、「導くなら理由を示せ」と言ったのか、で解釈が分かれる
- [[サール]]（1964）は「約束する」という[[制度的事実]]から「約束を守るべきだ」が出る、と反例を示そうとした
    - 制度的事実の中にすでに規範が入り込んでいるのでは、という再反論がある

AIとの関係
- [[アライメント]]は「AIが何をすべきか」を決める問題なので、is-ought問題を避けられない
- 「人々の過去の行動データから目的を学習する」は、事実から規範を引き出そうとする試み
    - [[6-Pack of Care]]の第1章「Many AI plans try to "learn the objective" from old data.」→ 共通の目標は変わり続ける人々の間の交渉なので、固定した正解を推測しても失敗する、と書いている
- [[Civic AI]]のマニフェストでの扱い（¶46-48、2026-10-20 時点のライブ版）
    - > Here, we face Hume's Is-Ought problem: No amount of accurate observation of how things are can derive a universally agreeable way things ought to be.
    - その上で、解決は薄い普遍原理ではなく[[厚いアライメント]]だ、とする
    - > Civic care offers a practical way forward — not by solving the Is-Ought problem, but by starting, as Joan Tronto puts it, "in the middle of things."
        - 問題を「解く」のではなく、民主的な価値へのすでにある約束の中から始め、互いに依存していることを真剣に受け止めたらその約束が何を求めるかを問う
    - 2026-02-21 の改訂（commit a559c4c）より前は「Civic Care is a bridge from "is" to "ought"」、つまり「架け橋になる」と書いていた
        - コミットメッセージは「Reframe Is-Ought bridge as starting within democratic commitments (Tronto's "in the middle of things"), not deriving values from facts.」
        - 事実から価値を導くと読める言い方をやめた形