---
title: "Zope期"
---

2003年にNAIST金谷研究室でZopeを使ってWebを構築し始めた時期


<img src='https://scrapbox.io/api/pages/nishio/opus5/icon' alt='opus5.icon' height="19.5"/> 「書き物」という一覧ページに、2003〜2005年ごろの記事が30件並んでいます。

[[NAIST期]]にほぼ包含される

関連:
- [[COREBlog期]]
    - COREBlogはZope上で動くブログシステム
- [[tDiary期]]
    - tDiaryはRubyのはずで、もちろんZopeの上で動かない。

prev: [[前Zope期]]

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> サーバがZopeなのは誰がやったのか、僕じゃないと思うが(ymasudaかな？)
<img src='https://scrapbox.io/api/pages/nishio/Opus5/icon' alt='Opus5.icon' height="19.5"/>
- Zope体験記の2003-11-02のエントリにこうあります:
    - > 最新のZopeをインストールしつつあったのだけど、最新のZopeであってもPython2.1どまりなんだってさ。こんなスクリプトを書いたら「global name 't' is not defined」って言われた。ネストされたスコープがサポートされてないんじゃないかな
- 導入初日からPython 2.2の言語機能（ネストスコープ）を当然のように使おうとして、Zope側の古さに文句を言っている——つまりZopeを触る前からPythonユーザーだったことがここから確定します。2003年秋に「PythonでWebコンテンツ管理をやりたい」と思ったら、[[Django]](2005)はまだ存在せず（他言語だと[[Ruby on Rails]]が2004）、Zopeがほぼ唯一の選択肢でした。Plone/Zopeブームの絶頂期で、日本にもZopeユーザー会があり和書も複数出ていた時代です。言語からの消去法でほぼ説明がつきます。
- 研究室サイト（kanaya.aist-nara.ac.jp/Zope/）の最古キャプチャは2004-02で、本人サイトのカウンタ起算（2004-01-23）とほぼ同時。「研究室が昔からZopeだったので合わせた」説は裏付けが取れず、むしろ自分のZope導入と研究室サイトのZope化が同時期——自分で立てて研究室ページも巻き取った可能性すらあります（2004-09に研究室の研究紹介ページを自分でリファクタリングしている）