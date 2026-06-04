---
title: "Tailscale"
---

2026-05-09
<img src='https://scrapbox.io/api/pages/nishio/Claude/icon' alt='Claude.icon' height="19.5"/>
- Mac に Tailscale をインストール
    - brew install --cask tailscale
    - open /Applications/Tailscale.app
- 起動後、メニューバーから Sign in（Google でも GitHub でも好きな IdP で）
- iPhone に Tailscale アプリを入れて、Mac と同じアカウントでログイン
- Admin Console で HTTPS を有効化
    - [https://login.tailscale.com/admin/dns](https://login.tailscale.com/admin/dns) を開いて Enable HTTPS をクリック

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
- iPhoneと手元のMacBookをVPNで繋いで出先でもMacBookで建てたサーバに接続できるようになるみたい
- Tailnet？と呼ばれる自分のVPNに接続するところでOAuth認証がかかるので、他人が入ってくる心配がない
    - [[ngrok]]の進化バージョン
- <img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>
    - Tailscaleは、自分のPC・スマホ・サーバー・NASなどを、安全なプライベートネットワークでつなぐサービスです。雑に言うと「設定がかなり簡単なVPN」ですが、従来型VPNとは少し構造が違います。
    - 中身は [[WireGuard]] という軽量なVPNプロトコルを使っています。Tailscaleはその上に、ログイン、端末管理、鍵交換、アクセス制御、NAT越えなどの仕組みを載せて、普通の人間が扱いやすくしたものです。公式にも、TailscaleはWireGuard上に構築され、鍵管理や接続確立を簡単にする管理プレーンを提供すると説明されています。
    - 重要なのは、Tailscaleは通常の「VPNサーバーに全通信を流す」方式ではなく、端末同士が可能なら直接つながるメッシュ型です。
        - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>なるほどね
