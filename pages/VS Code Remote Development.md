
- [【設定爆速】VS CodeのRemote Developmentを使ってSSH接続したEC2上のファイルを編集する ｜ Developers.IO](https://dev.classmethod.jp/etc/vs-code-remote-development-ec2/?fbclid=IwAR1OFTI57_SSOWQPqMGttmF_FW8cLtq19Y2pC55RizGGGCOwJsqzX3KSGSE)
- もう通常版で使える
- Remote Development 拡張を入れる
    - Remote - SSHも一緒に入る
![image](https://gyazo.com/6e6b0c72e8b59ad98e7e4d437a476cf4/thumb/1000)

- sshのコマンドを確認する
    - `$ ssh -i /Users/nishio/.ssh/***.pem ubuntu@54.**.**.**`
    - これを SSH targetsに追加する(プラスボタン)
        - SSHのconfigファイルに書き込まれる
        - 適宜編集して良い(歯車ボタン)
- プラス窓ボタンで接続
    - View > Terminal でターミナルを開けば普通のSSHみたいに使える
        - [Integrated Terminal in Visual Studio Code](https://code.visualstudio.com/docs/editor/integrated-terminal)
    - コンソールは複数タブ開ける
        - だけどtmux的なセッション維持はしないのでVSCodeのこのウインドウを閉じるとプロセスは死ぬ
    - リモートのどのディレクトリを開くか指定できる、デフォルトだとホームかな

[[VSCode]] Remote Development
