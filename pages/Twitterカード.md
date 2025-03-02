
[カードの利用開始 — Twitter Developers](https://developer.twitter.com/ja/docs/tweets/optimize-with-cards/guides/getting-started)
- Open Graphのタグとの組み合わせ方が末尾に書いてある
ts

```typescript
<meta name="twitter:card" content="summary" />
<meta name="twitter:creator" content="@nishio" />
<meta property="og:url" content="https://shinuwani.netlify.com/" />
<meta property="og:title" content="○年後に死ぬあなた" />
<meta property="og:description" content="漫画「100日後に死ぬワニ」を見てたら自分が何年後に死ぬのか気になったので作りました。" />
<meta property="og:image" content="https://shinuwani.netlify.com/shinuwani.jpg" />
```

- [シェアデバッガー - Facebook for Developers](https://developers.facebook.com/tools/debug/?q=https%3A%2F%2Fshinuwani.netlify.com%2F)
- [Card Validator | Twitter Developers](https://cards-dev.twitter.com/validator)


- Twitter Preview
    - ![image](https://gyazo.com/5b1094802c9149e4d37cf8cf46fc7552/thumb/1000)
- Real
    - ![image](https://gyazo.com/605989ee002c5ac2b889bbc79986f338/thumb/1000)



- Facebook Preview
    - ![image](https://gyazo.com/d4dd014e3710c224ce5c41dfaace9e1b/thumb/1000)
- Real
    - ![image](https://gyazo.com/a80db0cb4cc47f30c46d8a1c6ff4f85b/thumb/1000)

[[react-helmet]]を使う案もあったが、単独ページ単独ファイルなので直接headをいじる方がいいと判断した
