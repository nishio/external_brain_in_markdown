
from [/villagepump/2023/09/13](https://scrapbox.io/villagepump/2023/09/13)
- やっちゃうか？やめとくか？
    - という気持ち(何)
    - うーん
    - あ、たまたまケアレスミスで190個と832個に分かれてるな
    - 190個の側がReady
    - じゃあ天啓だということにしてこれをやっちゃうか
    - 概算で4万枚の画像をGyazoにアップロード
- `You have fired too many requests.`になってた

from [/villagepump/2023/09/14](https://scrapbox.io/villagepump/2023/09/14)
<img src='https://scrapbox.io/api/pages/villagepump/nishio/icon' alt='/villagepump/nishio.icon' height="19.5"/>
- GyazoへのUpload、1万件くらいで`Too many requests`になってしまった
    - [https://gyazo.com/api/docs/errors](https://gyazo.com/api/docs/errors)
    - > APIには使用制限があり、12,500回/日です。
    - >  使用制限を超えた場合、ResponseのStatus Codeで429が返ります。
    - だって<img src='https://scrapbox.io/api/pages/villagepump/takker/icon' alt='/villagepump/takker.icon' height="19.5"/>
    - そっかー<img src='https://scrapbox.io/api/pages/villagepump/nishio/icon' alt='/villagepump/nishio.icon' height="19.5"/>
        - まあ無制限にアップロードしてOCRとして使われると困るから制限があるのは仕方ない
        - 12500だとまあ、普通のユースケースなら問題ないし。
- 「とりあえず画像を4万件アップロードしてみよう」はできないことがわかったので、ネクストアクションを考える
- UploadだけでなくGetもAPI上限の対象だった
- つまりUploadで使い切った現状、Gyazo側にOCR済みのテキストはあるけど取得できないw
- 日常的なプロセスとしては「1日に250ページの本を25冊追加できる」は十分すぎる上限なのだが、過渡期にどうするかが問題
- まあ、とりあえず24時間くらい経つまで後段の実験ができないから待つか

from [/villagepump/2023/09/15](https://scrapbox.io/villagepump/2023/09/15)
- Gyazoに追加課金したらAPIのQuota増えないかな
- Gyazoのアカウントを10個くらい契約したら10倍API使えるよな
    - 天才<img src='https://scrapbox.io/api/pages/nishio/takker/icon' alt='takker.icon' height="19.5"/><img src='https://scrapbox.io/api/pages/nishio/takker/icon' alt='takker.icon' height="19.5"/>
    - Gyazo Pro、30日無料だ、いくつでも作れるぞ(コラ)<img src='https://scrapbox.io/api/pages/villagepump/nishio/icon' alt='/villagepump/nishio.icon' height="19.5"/>
    - 後から一つのアカウントにマージすることができないので「あれ？ないな？」になりそうだなぁ
        - そうだった。無念<img src='https://scrapbox.io/api/pages/nishio/takker/icon' alt='takker.icon' height="19.5"/>
        - 個人のGyazoの画像を[[Gyazo Teams]]に移行することはできるらしい<img src='https://scrapbox.io/api/pages/villagepump/nishio/icon' alt='/villagepump/nishio.icon' height="19.5"/>
            - 「この10個を移行してください」「じゃ、9人解約しますね」酷い
            - Gyazo Team、最低でも月額5000円からだった
- 最終的にGyazo Proに一本化された方が考えることが減っていいだろうと思ったんだが、移行期にAPIのQuotaのせいで50日程度掛かる見積もり…

from [/villagepump/2023/09/17](https://scrapbox.io/villagepump/2023/09/17)
- `page.lines must be less than 10000 lines`
    - (~_~)
    - インポートできないだけなのか、超えられないのかどちらだろう
    - 9000行くらいで分割するか
- 14274項目、2.45GB、50冊
    - 3日掛かった
- 長いページを分割してインポートする実装に変えた
    - できた

from [/villagepump/2023/09/17](https://scrapbox.io/villagepump/2023/09/17)
- 書籍をGyazoにつっこむ話
    - GyazoのQuota不足で不完全なデータになってたのを全部直し終わった
        - 2.5日掛かった
    - 新しく処理する本は20冊ずつのグループを3つ作った
        - 予想通りなら1日1グループずつ処理できるはず
        - まあ1000冊あるので予定通りだとしても50日コースなわけだが…
        - 「ぶっ壊れたデータを修復して…」とか「今日はもう使い切っちゃったから…」とか考えるのめんどくさいしね
        - とかいって、20冊の中にやたら長い本があってやっぱりQuotaを超える可能性も…
        - リカバリーモードを実装してあるからその場合は翌日にリカバリーしてから新しいのを走らせる

2023-09-19
- 9時間も前にアップロードしたのにOCRがされてない画像が数枚ある
- 確率でOCRのAPIコールが失敗して、適切にリトライされない現象っぽいな…
- 結局ラストの1冊の中の4ページだけがその症状だった
    - "OCR not available"で埋めた、どうするべきか
