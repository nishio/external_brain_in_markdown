---
title: "HTTPSサービスを他のHTTPSサービスに埋め込む"
---

結論
- 埋め込もうとしたサービスが[[x-frame-options]]: SAMEORIGIN だったので無理

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>httpsのサービスを他のhttpsのサービスに埋め込めるかどうかはheaderのどれを見ればわかる？
<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>
HTTPSサービスを他のHTTPSサービスに埋め込む可否は、### X-Frame-Options
ヘッダー（および場合によっては### Content-Security-Policy
の### frame-ancestors
ディレクティブ）で確認できます。
- X-Frame-Options:
    - `DENY` または `SAMEORIGIN` が設定されていると、他サイトでの埋め込みが制限されます。
- Content-Security-Policy (frame-ancestors):
    - より詳細な制御が可能です。

