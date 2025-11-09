---
title: "Cloudfrare Tunnel"
---

[[ngrok]]的なやつ

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>ngrok的なことを2025年にやる場合のおすすめは？
<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>西尾さん、2025年版の「ngrok的にローカルを外に出す」選択肢を用途別にまとめました（どれも実運用でよく使われています）。
- まず結論（用途別おすすめ）
    - ゼロ設定で安定・無料枠重視 → Cloudflare Tunnel ([[cloudflared]])。常時公開やSSH/任意TCPもOK、アウトバウンド接続だけで安全。Zero Trust 認証も載せやすい。
...
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>もう少し補足するとローカルで動いている開発中のサービスにスマホからアクセスしたい、Cloudfrare Tunnel興味ある
<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>Cloudflare Tunnel（旧 Argo Tunnel）を使うと、あなたのローカル環境で動いている開発中サービスをスマホや他端末から安全にアクセスできるようになります。


Macでinstall
- `$ brew install cloudflare/cloudflare/cloudflared`

開発サーバが`http://localhost:5173/`で動いている
- `$ cloudflared tunnel --url http://localhost:5173/`
- > Your quick Tunnel has been created! Visit it at (it may take some time to be reachable):
- >  aaa-bbb-ccc-ddd.trycloudflare.com

スマホでアクセス
> Blocked request. This host ("aaa-bbb-ccc-ddd.trycloudflare.com") is not allowed.
> To allow this host, add "refer-hearts-throwing-phenomenon.trycloudflare.com" to `server.allowedHosts` in vite.config.js.
<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>Cloudflareトンネル経由でアクセスしているようですね。[[Vite]]の設定でこのホストを許可する必要があります。
→見れた
しかしいまどきフロントエンドからAPIを叩くからそれもトンネルする必要がある

API_BASE_PATHに書いたりとかめんどくさい
- とりあえず無理やり2つトンネルしたけど、王道はnginxで一つのドメインに束ねてそれをトンネルする方法だね
- 無理やりだけどiPhoneから使うことができた
