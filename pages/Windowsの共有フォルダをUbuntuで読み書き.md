
`$ mount -t cifs -o username=***,password=***,uid=$(id -u),gid=$(id -g) //*1*/Users/nishio/Documents/shared ~/shared`
- *1*: WindowsマシンのIPアドレス
- あらかじめファイル共有しておく

読むだけなら`uid=$(id -u),gid=$(id -g)`がなくてもいいんだがディレクトリのオーナーがrootになるのでファイルを作ろうとしてエラーになったりする

[[Windows]]の[[共有フォルダ]]を[[Ubuntu]]で読み書き
[[cifs]]: [[Samba]]
[[パーミッション]]
