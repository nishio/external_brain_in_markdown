---
title: "SubRISC+"
---

[東工大、IoT向けCPUアーキテクチャ「SubRISC+」。エネルギー効率3.8倍 - PC Watch](https://pc.watch.impress.co.jp/docs/news/1307882.html)
> 命令数を4つに限定することで小型/低消費電力化を図った。
この4つとは何か？と話題になったので調べた。
- 引き算して結果が負だったらジャンプ
- ビットAND
- シフト
- メモリアクセス(load/store？、詳細は下記)
の4つ。もともと一つ目の命令だけでチューリング完全であることが知られていた。(OISC: [One-instruction set computer](https://en.wikipedia.org/wiki/One-instruction_set_computer#Subtract_and_branch_if_negative))

[エッジ端末に適した小型省電力プロセッサを実証 従来比3.8倍のエネルギー効率でヘルスケアIoTに道 | 東工大ニュース | 東京工業大学](https://www.titech.ac.jp/news/2021/048954.html)からリンクされてた論文の記述(太字は西尾による)
> Here we briefly explain the basics of SubRISC+ to the extent of highlighting our contributions in this paper. SubRISC+ was developed on the basis of a one-instruction set computer (OISC) whose unique instruction is ‘‘subtraction and branch on negative’’ that is capable of realizing any operations and hence is Turing complete. By extending the instruction set architecture (ISA) of this OISC, SubRISC+ handles four instructions (subtraction, bitwise AND, shift, and memory access) that can be flexibly expressed in either 16 bits (for compactness) or 32 bits (to support an immediate value or branch) to improve computing and power efficiency while retaining simplicity with a very limited circuit overhead.
- [https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=9133073](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=9133073)
- ![image](https://gyazo.com/f67cc8123a482f7b21279f8d29bcae62/thumb/1000)
    - AとBがnot equalならジャンプ、という命令は「AからBを引いて負ならジャンプ、BからAを引いて負ならジャンプ」で表現できる
    - ビット演算のnotはフルビット立ってる-1からの引き算で表現できる

無条件ジャンプ
- ![image](https://gyazo.com/567d984c3e024ff3a3c970f2cdbc82c1/thumb/1000)
- [https://en.wikipedia.org/wiki/One-instruction_set_computer#Subtract_and_branch_if_negative](https://en.wikipedia.org/wiki/One-instruction_set_computer#Subtract_and_branch_if_negative)
- 正の数が入ってるPOSと、ゼロが入ってるZを用意する
- 無条件ジャンプは「`Z - POS`が負ならジャンプ」で実現できる
- ジャンプ先で「`Z = Z - Z`」を実行してゼロに戻しておく

メモリアクセス命令について
- 論文には「メモリアクセス」としか書いてないので詳細がわからない
- 1つだけ？片方向にしか動かせない？と思ってたが光成さんから「x86ならloadとstoreあわせて一つのmov命令」との指摘があったので、確かにそれなら「メモリアクセス」の一言で済ませそうと思った
- 別の意見
    - >  [kazuho](https://twitter.com/kazuho/status/1364492476740820992) レジスタからのストア命令じゃないかなと思った。回路規模を抑えるって意味で、subnegの2引数をメモリとレジスタ、デスティネーションをレジスタにして、ストアを別命令にするあたりがバランスいいんじゃないか
    - さらに追記
        - [https://twitter.com/kazuho/status/1364537398600880128?s=21](https://twitter.com/kazuho/status/1364537398600880128?s=21)
