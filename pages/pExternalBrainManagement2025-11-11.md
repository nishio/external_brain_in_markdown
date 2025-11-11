---
title: "pExternalBrainManagement2025-11-11"
---

[[イラストポートフォリオ]]
[[西尾泰和の落書き]]

xkcdみたいなイラストまとめViewを作ろうと考えている。URLを/illust/ja/<page>とするか/ja/illust/<page>とするか迷っている

<img src='https://scrapbox.io/api/pages/nishio/Claude/icon' alt='Claude.icon' height="19.5"/>
⏺ URL設計について、一般的には /ja/illust/<page> の方が推奨されます。理由は以下の通りです：
/ja/illust/<page> を推奨する理由
1. 国際化（i18n）のベストプラクティス
- 言語コードを最上位に置くのがWeb標準
- Google等の検索エンジンも推奨
- Next.jsのi18nルーティング機能と自然に統合できる

実装を相談しながら進められるのはいいな<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>

2. next.config.jsのi18n設定（Next.js 10+）
js

```javascript
// next.config.js
module.exports = {
i18n: {
locales: ['ja', 'en'],
defaultLocale: 'ja',
},
}
```

この設定を使うと：
- 自動で/ja/page、/en/pageにルーティング
- デフォルト言語なら/pageも許可
- Accept-Languageヘッダーで自動リダイレクト

へー、そんなのがあるのか<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>


別件、devinでバグフィックスできた
- [https://github.com/nishio/mem/pull/1](https://github.com/nishio/mem/pull/1)
- なのでこれでたとえば出先でスマホからSlack経由でリクエストして作業させることができる

---
CCがPlanを書いた
あとはDevinに任せる
- [https://github.com/nishio/external_brain_management/blob/main/docs/diary/2025-11-11-2-PLAN.md](https://github.com/nishio/external_brain_management/blob/main/docs/diary/2025-11-11-2-PLAN.md)
- [https://github.com/nishio/external_brain_management/blob/main/docs/diary/2025-11-11-3-ACTIVITY_REPORT.md](https://github.com/nishio/external_brain_management/blob/main/docs/diary/2025-11-11-3-ACTIVITY_REPORT.md)
- だいたい問題なく動いている
    - [https://mem.nhiro.org/ja/illust](https://mem.nhiro.org/ja/illust)

----


![image](https://gyazo.com/2f6b7b70e0a4c8ff0d85aa53edc0761b/thumb/1000)
⚠️ 残っている「modified content」について
modified:   modules/external_brain_in_markdown (modified content, untracked content)
これはmacOSのUnicode正規化の問題です：
- ファイル名の大文字小文字の違い（Bashi.md vs bashi.md）
- 濁点・半濁点の表現方法の違い（合成文字 vs 分解文字）

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
- git checkoutしただけでmodificationが発生する、キモい

