
2022/9/22
僕のメインマシンはMacBookだが、Stable Diffusionの環境を構築するにあたってまともなGPUがあるのがWindowsのゲーミングPCだけだったのでWSL2で環境構築した。
そのゲーミングPCにMacBookからSSHして操作できるようにしたい。

WSL1と異なりWSL2ではネットワークが分離されている。なので基本的にはWindows側でWSL側にポートフォワーディングする。

[Linuxがほぼそのまま動くようになった「WSL2」のネットワーク機能：Windows 10 The Latest - ＠IT](https://atmarkit.itmedia.co.jp/ait/articles/1909/09/news020.html)
- [[Hyper-V]]のネットワークのしくみから書いてて親切
- [[localhost]]が単一の自分自身を指すアドレスではなく、127.0.0.0という特殊なネットワークの中の一つで、異なるIPアドレスでもlocalhost経由でアクセスできる、という仕組みは知らなかった

段階を追って確認していく

bashで下記を実行してHTTPサーバを8000番でたてる
- `$ python -mhttp.server`
Windowsのブラウザで下記にアクセスする
- [http://localhost:8000/](http://localhost:8000/)
見れた！一方で
- [http://192.168.1.13:8000/](http://192.168.1.13:8000/)
これは確かに見えない。なるほど。こういうことね
![image](https://gyazo.com/1b783dd098acf7e6a56850d38703d06f/thumb/1000)

ポートフォワーディングの状態を確認するために管理者権限PowerShellを立ち上げらる
powershell

```
> netsh interface portproxy show v4tov4
```


powershell

```
> netsh interface portproxy add v4tov4 listenport=8000 connectaddress=localhost

> netsh interface portproxy show v4tov4
 ipv4 をリッスンする:         ipv4 に接続する:

 Address         Port        Address         Port
 --------------- ----------  --------------- ----------
 *               8000        localhost       8000

> sc start iphlpsvc
```

これで
Windowsのブラウザで下記にアクセスして見れるようになった
- [http://192.168.1.13:8000/](http://192.168.1.13:8000/)
一方でMacBookのブラウザからは見れない、これはつまりファイヤーウォールで弾かれてるのだな

「Windowsファイヤーウォールによるアプリケーションの許可」ではアプリを指定することになる❌。
今回はポートを指定したいので「詳細設定」「受信の規則」「規則の追加」「ポート」と進む
![image](https://gyazo.com/cd361182c52a789fdf641a2eb1467619/thumb/1000)
![image](https://gyazo.com/d36739f795fbd1f7962939a102f95b41/thumb/1000)
これでMacBookからもブラウザでアクセスできるようになった。

次はSSHの設定。
まずbashで
bash

```
$ ssh localhost
ssh: connect to host localhost port 22: Connection refused
```

つながらない、つまりSSHサーバが起動してない
公開鍵をauthorized keysに書いて
`$ sudo service ssh start`
bashでつながるようになった

MacBookからSSHするとタイムアウト…ファイヤーウォールの22番ポートは開けたけど…あっ、ポートフォワーディングが8000番だけしかやってなかった。22番もポートフォワードして無事MacBookから繋がるようになった。

---
2022-09-25
- > なぜかWSLにSSHで繋がらなくなってしまってゲンナリしてる

2022-09-26
powershell

```
netsh interface portproxy show v4tov4
ipv4 をリッスンする:         ipv4 に接続する:
Address         Port        Address         Port
--------------- ----------  --------------- ----------
*               22          localhost       22
*               8000        localhost       8000

```

bash

```
$ python -mhttp.server
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
```

[http://localhost:8000/](http://localhost:8000/) NG

bash

```
$ ip -4 address
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
6: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    inet 172.28.171.149/20 brd 172.28.175.255 scope global eth0
       valid_lft forever preferred_lft forever
```


[http://172.28.171.149:8000/](http://172.28.171.149:8000/) OK

localhostの転送が働いてなさげ

[windows - Localhost refused to connect on WSL2 when accessed via https://localhost:8000/ but works when using internal WSL IP adress - Stack Overflow](https://stackoverflow.com/questions/69926941/localhost-refused-to-connect-on-wsl2-when-accessed-via-https-localhost8000-b)
> When it's working normally, as you are clearly aware, the "localhost forwarding" feature of WSL2 means that you can access services running inside WSL2 using the "localhost" address of the Windows host.
>
>  Sometimes, however, that feature breaks down. This is known to happen when you either:
- >  Hibernate
- >  Have the Windows "Fast Startup" feature enabled (and it is the default). Fast Startup is a pseudo-hibernation which triggers the same problem.
>  Typically the best solution is to disable Hibernation and Fast Startup. However, if you do need these features, you can reset the WSL localhost feature by:
>
>  Exiting any WSL instances
>  Issuing wsl --shutdown
>  Restarting your instance
>  It's my experience that localhost forwarding will work after that.
WSLの再起動は試してみたけどダメだった

[Fixing WSL2 localhost access issue - abdus.dev](https://abdus.dev/posts/fixing-wsl2-localhost-access-issue/)
> Localhost redirection often fails for some reason, such as when PC sleeps and wakes up, and localhost access to Linux services does not work anymore.

結論「WSL2のlocalhost bindingはすぐ壊れるから信用しないでIPアドレス直接指定にする」

powershell

```
> netsh interface portproxy set v4tov4 listenport=8000 connectaddress=172.28.174.254
> netsh interface portproxy set v4tov4 listenport=22 connectaddress=172.28.174.254
```


MacのブラウザからHTTPサーバに繋がるようになった
sshはつながらない、これはWSLを再起動してsshdが起動してないから
起動した、つながるようになった

2022-10-03
[SSH into a WSL2 host remotely and reliably | by Gilad Lekner | Medium](https://medium.com/@gilad215/ssh-into-a-wsl2-host-remotely-and-reliabley-578a12c91a2)
[WSL2のUbuntuにsshできるようにする](https://sunday-morning.app/posts/2020-07-16-wsl2-ubuntu-ssh)

2022-10-10
bashの中でip -4 address
そのアドレスを管理者PowerShellの方で
PS C:\WINDOWS\system32> netsh.exe interface portproxy set v4tov4 listenport=22 connectaddress=172.22.33.108

PS C:\WINDOWS\system32> netsh.exe interface portproxy set v4tov4 listenport=8000 connectaddress=172.22.33.108
>  netsh interface portproxy show v4tov4

ipv4 をリッスンする:         ipv4 に接続する:

Address         Port        Address         Port
--------------- ----------  --------------- ----------
*               22          172.22.33.108   22
*               8000        172.22.33.108   8000

>  sc.exe start iphlpsvc
[[SC]] StartService FAILED 1056:

サービス インスタンスは既に実行されています。


