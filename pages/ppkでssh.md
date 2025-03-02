---
title: "ppkでssh"
---

- *.ppkのファイルを渡されてこれでサーバに入れと言われたがssh -iで指定してもinvalid formatになる件
- ppkはPutty形式らしい
- openssh形式に変換する必要がある [ref](https://superuser.com/questions/232362/how-to-convert-ppk-key-to-openssh-key-under-linux)
    - `puttygen INPUTFILE.ppk -O private-openssh -o OUTPUTFILE`