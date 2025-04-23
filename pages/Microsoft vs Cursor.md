---
title: "Microsoft vs Cursor"
---

[[Microsoft]] vs [[Cursor]] ― [[OSSエコシステム]]を揺るがす「[[機能模倣]]」と「[[締め出し]]」論争

> [kinopee_ai](https://x.com/kinopee_ai/status/1913975162288082970) Microsoft は昨秋の Cursor のマルチファイル編集機能を丸パクリから始まって、恥ずかしげもなく、エージェントはモード名まで丸パクリ。Mac OS パクリと酷似。
>  無料プラン作って登録者が増えたと喜び、今度はマーケットプレイスからフォーク組を排除。
>  Evil な企業と批判された歴史をお忘れのようで。

> [nuits_jp](https://x.com/nuits_jp/status/1914107853343973589) 気になってたから調べてみたけど、拡張マーケットプレイスをCursorが直接利用することは規約違反なのでは？
>  [Microsoft Visual Studio Marketplace and NuGet.org
>  Terms of Use []](https://cdn.vsassets.io/v/M253_20250303.9/_content/Microsoft-Visual-Studio-Marketplace-Terms-of-Use.pdf)
>
>  そもそもOSSをフォークした上、クローズで開発して莫大な利益をあげ、OSSに還元していないCursor側が言える立場ではないのでは？

<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>
### 論点を5行で整理
1. ### Cursorの先行機能
- VS CodeフォークのCursorは2024年から「AIエージェント (Composer/Agent Mode)」とマルチファイル同時編集を売りにして急成長。
2. ### Microsoftの追随と名称まで類似
- 2025年4月、GitHub Copilotに同名のAgent Modeと一括編集機能が正式実装され、UI・語彙がCursorと酷似すると開発者が指摘。
3. ### Marketplace利用禁止で事実上の締め出し
- 直後にMicrosoftは公式拡張に「VS Code以外では動作不可」フラグを追加。
- CursorでC/C++拡張などが動かなくなり、コミュニティは「[[抱擁→拡張→排除]](E³)」と批判。
4. ### 反対側の主張
- ― Microsoft擁護: 規約は以前からあり、Cursorは違反して公式Marketplaceを横取りしていた。
- ― Cursor批判: OSS (VS Code MIT)を基盤にしながら改良部分はクローズドで高額SaaS化し、コミュニティへ還元が乏しい。
5. ### OSSカルチャー上の評価
- Microsoft: 巨大プラットフォームの支配力でフォークを封じ込め、囲い込み傾向。
- Cursor: ライセンス上は合法だが、規約違反と“ただ乗り”の印象。
- 結論: どちらも理想的なOSS市民とは言えず、利用者はOpen VSXなど開かれた代替エコシステムの充実を求める段階。

### 私の感想
企業の商業判断とOSS精神のギャップが顕在化した典型例。Microsoftは影響力が大きい分、公平性と透明性を示す責任も大きい。一方Cursorも「OSS利用→クローズド利益化→規約無視」という弱点がある。両陣営がコミュニティとの協調姿勢を強め、拡張APIやマーケットをオープン規格で相互運用できるよう歩み寄ることが、開発者全体の利益になると考える。

<img src='https://scrapbox.io/api/pages/nishio/DR/icon' alt='DR.icon' height="19.5"/>[https://chatgpt.com/share/6808bdb0-8218-8011-94a4-8e1b31bbeb1e](https://chatgpt.com/share/6808bdb0-8218-8011-94a4-8e1b31bbeb1e)

