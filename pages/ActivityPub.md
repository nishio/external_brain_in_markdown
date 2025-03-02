
from [/villagepump/ActivityPub](https://scrapbox.io/villagepump/ActivityPub)
![image](https://gyazo.com/28b76540c1d91aa8dbb74aee0260a0c1/thumb/1000)
[https://github.com/w3c/activitypub](https://github.com/w3c/activitypub)
- W3C勧告: [ActivityPub](https://www.w3.org/TR/activitypub/)
- [[Mastodon]], [[Fedibird]], [[GNU Social]]などの[[Fediverse]]的Twitterを相互接続するためのプロトコル

<img src='https://scrapbox.io/api/pages/villagepump/nishio/icon' alt='/villagepump/nishio.icon' height="19.5"/>
- 昔RSSの時代には更新情報が発信者側のOUTBOXに置かれて読者側のRSSリーダー側がGETしてた、それからSlack通知の時代が来て発信者側のサービスがSlackのAPIにPOSTをするようになった、でも間のキューをどちらかのサービスに密結合なものとして考えるのはやめようよ、ということなのかな？
- ![image](https://gyazo.com/ec8d7baedec8f153cf4f0c6ac62fb54a/thumb/1000)
- ![image](https://gyazo.com/5992102a9b61924dfcd793209563dc8d/thumb/1000)


<img src='https://scrapbox.io/api/pages/villagepump/nishio/icon' alt='/villagepump/nishio.icon' height="19.5"/>
- 詳しい人による最小限の実装の解説っぽい
    - [第59回 Fediverse入門―非中央集権型SNSサーバを作ろう！（1） | gihyo.jp](https://gihyo.jp/dev/serial/01/perl-hackers-hub/005901)
    - [[HTTP Signatures]]
    - [[リモートフォロー]]
        - ユーザー名からアクター情報URLへの変換
        - 慣習的に[[Web Host Metadata]]と[[WebFinger]]によるやりとり
    - ローカルにフォロワーリストを持って、その各フォロワーのinboxに対してPOSTをする
        - inboxは他のサービスになり得るわけだ、なるほど
        - その柔軟性の代わりに「投稿頻度×フォロワー数」に応じたコストが掛かる
