---
title: "AIの役割の明確化が大事"
---

> 一般論としては「[[AIボット]]に与える『[[役割]]』や『[[目的]]』が重要」という気持ちがしている<img src='https://scrapbox.io/api/pages/enchi/nishio/icon' alt='/enchi/nishio.icon' height="19.5"/>


from [/enchi/AIの入れ方](https://scrapbox.io/enchi/AIの入れ方)
AIの入れ方
<img src='https://scrapbox.io/api/pages/enchi/nishio/icon' alt='/enchi/nishio.icon' height="19.5"/>
- ネクストアクションはここにAIを入れることでは？と思っている
- まだ何が行われるかは明確ではない
    - が、[[エンジニアの知的生産術]]の概念が
    - 「[[書籍としてのエンジニアの知的生産術]]」
    - →「[[Scrapbox上のコミュニケーションの場としてのエンジニアの知的生産術]]」
    - →「[[AIと人間の参加する場としてのエンジニアの知的生産術]]」
    - みたいに発展していきそう
- どういう入れ方をしたらいいかは少し悩んでいる<img src='https://scrapbox.io/api/pages/enchi/nishio/icon' alt='/enchi/nishio.icon' height="19.5"/>
    - [[Incremental Reading]]関連しそう

一般論としては「[[AIボット]]に与える『役割』や『目的』が重要」という気持ちがしている<img src='https://scrapbox.io/api/pages/enchi/nishio/icon' alt='/enchi/nishio.icon' height="19.5"/>
- 日々更新があるわけではないプロジェクトでAIが日々更新するとウザそう
- 毎日1ページ更新するより、週1で7ページ更新する方がいい説

この書籍のレビューフェーズを始める前に書いた[[Scrapboxをもっと活用する案]]が浮かび上がってきて再度読んだ<img src='https://scrapbox.io/api/pages/enchi/nishio/icon' alt='/enchi/nishio.icon' height="19.5"/>
- 「再度発散フェーズをやってもスケジュールに収まらない」がやらなかった理由
- であれば、今こそ[[再度発散フェーズ]]をやるといいのでは
- では「[[発散フェーズ]]」とは何か？


from [/omoikane/雑談ページ5](https://scrapbox.io/omoikane/雑談ページ5)
2023-08-31
<img src='https://scrapbox.io/api/pages/omoikane/nishio/icon' alt='/omoikane/nishio.icon' height="19.5"/>
- omoikaneのAIをどうするか再考中
- きちんと問わなければならない
- 「このプロジェクトにAIがいることで、あなたは何がどうなるとよいのですか？」
- [[AIの役割の明確化が大事]]は？
    - AIがみんなの書いたAI小説を読んで感想を書く？
    - AIがいろんな観点でAI小説を書く？
...
- [Github](https://github.com/nishio/omoikane-embed/commit/3f87c4c6b769a75b5012b70e71e6efed1e32676a)
- [[Omoikane Bot]]がランダムに1ページを選んで末尾に感想を加筆する実装に変わりました
    - 小説に限定することもないかなと。
- 必要とされている役割は「小説を読んで感想を書く」なのではないかという仮説


from [/unnamed-project/雑談ページ9](https://scrapbox.io/unnamed-project/雑談ページ9)
<img src='https://scrapbox.io/api/pages/unnamed-project/nishio/icon' alt='/unnamed-project/nishio.icon' height="19.5"/>
- こちらのAIにも改めて「[[AIの役割の明確化が大事]]」を考えてみる
    - 文脈: [/omoikane/雑談ページ5#64f05875aff09e0000cfc497](https://scrapbox.io/omoikane/雑談ページ5#64f05875aff09e0000cfc497)
- 複数のトピックが混ざっているページ(雑談ページが代表的)を分割する役割かなと思っている
- 多分「100ページになったら」という呪いによって、一つのページにコンテンツを押し込み、切り出さない圧力が発生した
- そのことによって切り出されてないページがたくさんある
- チャットを与えたときに話の内容で分割してサマリーをつける研究
    - [[MemoChat]]
    - Scrapboxのツリーで試してみたんだがまずは基本的にツリーで分割することがわかった
    - なのでツリーを取ってページに分割？
- 半自動で最も長いページの末尾の分割を提案するのができた
    - 最も長いページ: 雑談3 sustainしながら実が熟すのを待つ (15935 tokens)
- 今日はこの辺で。
- この切り出し良いと思った<img src='https://scrapbox.io/api/pages/unnamed-project/yits-khawk'9483/icon' alt='/unnamed-project/yits-khawk'9483.icon' height="19.5"/>
