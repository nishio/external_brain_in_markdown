
[/villagepump/2023/03/29#64241b37e1daa500001c217b](https://scrapbox.io/villagepump/2023/03/29#64241b37e1daa500001c217b)
from [/villagepump/2023/03/29](https://scrapbox.io/villagepump/2023/03/29)
- deploy先は[[Heroku]]かな<img src='https://scrapbox.io/api/pages/villagepump/takker/icon' alt='/villagepump/takker.icon' height="19.5"/>
    - です！Herokuを想定した設定ファイルを入れています<img src='https://scrapbox.io/api/pages/villagepump/shoya140/icon' alt='/villagepump/shoya140.icon' height="19.5"/>
        - [Socket Mode](https://api.slack.com/apis/connections/socket)を使っているのでSlackの設定を変更することなくローカルPCなどで試すことも可能
        - 自分はとりあえずHerokuの[[Eco dyno]]で走らせている
        - [[Herokuの30秒タイムアウト]]で死んでしまうことが…<img src='https://scrapbox.io/api/pages/villagepump/nishio/icon' alt='/villagepump/nishio.icon' height="19.5"/>
        - 30秒以上かかっても大丈夫なように[[Worker dyno]]を使っています<img src='https://scrapbox.io/api/pages/villagepump/shoya140/icon' alt='/villagepump/shoya140.icon' height="19.5"/>
        - なるほど！<img src='https://scrapbox.io/api/pages/villagepump/nishio/icon' alt='/villagepump/nishio.icon' height="19.5"/>
