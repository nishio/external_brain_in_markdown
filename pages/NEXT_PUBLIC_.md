---
title: "NEXT_PUBLIC_"
---

<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>Next.jsなどのフロントエンド環境では、process.envはビルド時に埋め込まれるもので、セキュリティ上、全ての環境変数がクライアント側に露出されるわけではありません。通常、NEXT_PUBLIC_で始まる環境変数だけがクライアント側に注入されるため、直接JSON.stringify(process.env)しても{}と表示されるのは仕様通りです。
