---
title: "NextJSでGoogle Analytics"
---

`import Script from 'next/script'`すればいい
- [next-script-for-ga | Next.js](https://nextjs.org/docs/messages/next-script-for-ga)

ただし2021/06/16 未明にリリースされた v11 以降の Next.js である必要がある
- [【Next.js 11】next/script には JavaScript の基本がつまっていた](https://zenn.dev/aiji42/articles/9a6ab12ab5f6e6)
- Can't resolve 'next/script'になる
- `npm install react@latest react-dom@latest next@latest`したらできた

[[NextJS]]で[[Google Analytics]]
