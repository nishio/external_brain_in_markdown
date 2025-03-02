
![image](https://gyazo.com/66e8059b7562df5f0bc249400e0b9661/thumb/1000)

- [[Builderscon 2018]]でもらった[[デジタル名札]]
- 詳しいことをデジタル名札のページに書いていくのもなんだから分けた
- [電子名札開発での異常な努力 または私は如何にして心配するのを止めて『謎ガジェット』を作るようになったか - builderscon::blog](https://blog.builderscon.io/entry/2018/08/09/100000)

2018-09-11
- [electronic_badge_2018/HOW_TO_LOGIN.md at master · builderscon/electronic_badge_2018](https://github.com/builderscon/electronic_badge_2018/blob/master/docs/HOW_TO_LOGIN.md)
- > ログインパスワード : NAFUDAドライブ内 default_passwd.txtに記載されています。
    - default_passwd.txt missingってエラーメッセージが表示されてる
- ３通りの接続方法を眺めて、Serialを選択
    - `touch /Volumes/NAFUDA/enable_g_serial`
    - 再起動しても/dev/cu.usbmodem1421が現れない
- touch後にFinderでenable_g_serialの存在を目視した後、取り出し、電源断、電源再接続して下記の画面
    - ![image](https://gyazo.com/118b34584be90ff796238979b6b81069/thumb/1000)
- うーん、シリアルモードへの変更がうまく動いていない模様
- UARTをつなぐしかないかな
- ダメ元でdefault_passwd.txtを生成して再起動してみた
    - パスワードの存在は認識された
- 改めて`touch /Volumes/NAFUDA/enable_g_serial`
    - やっぱりg_mass_strageモードのまま
- 続きはUARTで。
- フィードバック
    - > 再起動した後にNAFUDAドライブからは正しくenable_g_serialのファイルきえていますでしょうか？
    - >  正しく消えているのに反映されない場合、Macでtouch後に20秒位まってからeject作業を開始してみて下さい！write cacheが間に合わない？現象を認識しています!
- 次回これをまず試す

やりたいこと
- 20秒待ってejectをまず試す
- SSHでログイン
    - UARTでログイン
- Jenkinsをインストール
- Githubにpushしたら(ケーブル繋いで書き込んだりとかしなくても)RasPiの中のソースコードが更新されて欲しい
- ボタンを付ける
- LEDを付ける
- ポモドーロタイマーにする
