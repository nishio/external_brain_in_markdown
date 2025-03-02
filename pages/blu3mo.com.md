
from [/villagepump/2023/10/22](https://scrapbox.io/villagepump/2023/10/22)
<img src='https://scrapbox.io/api/pages/villagepump/blu3mo/icon' alt='/villagepump/blu3mo.icon' height="19.5"/>
- [http://blu3mo.com/](http://blu3mo.com/)
    - Scrapboxの英訳サイトをはやした（数ヶ月ぶり3度目）
    - 作ってはクオリティに納得いかず放置を繰り返していたけど、これなら人に紹介できそう
    - 実装
        - 翻訳をキャッシュして更新時は差分だけ訳す
        - gpt-3.5-turboを使っている
        - 中身をmarkdownに変換して、翻訳して、それを[[Quartz]]を使って公開している
            - markdownならgptが箇条書きやフォーマットを理解した上で訳してくれるので良い
            - [[ScrapboxToObsidian]]、[[QuartzでObsidian Vaultを公開]]、[[ScrapboxTranslator v1]]など過去の実装が役に立って嬉しい<img src='https://scrapbox.io/api/pages/villagepump/blu3mo/icon' alt='/villagepump/blu3mo.icon' height="19.5"/>
        - [[ScrapboxTranslator v2を作る]]のpromptはやめた
            - hallucinationが多すぎた
    - これからやること
        - 一部の面白がってもらえそうなページをピックアップして翻訳修正 & 見やすい場所に置く
        - ポートフォリオサイトとしてのページを追加する
        - 英語Twitterアカウントと連携
    - 事故が怖いのでrepoはprivateにしてますが、仕組み使いたければ連絡ください
        - 気になるー<img src='https://scrapbox.io/api/pages/villagepump/nishio/icon' alt='/villagepump/nishio.icon' height="19.5"/>

[[Scrapbox Translator v3]]
[[ScrapboxTranslator]]
