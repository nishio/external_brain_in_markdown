
from [/villagepump/2022/03/25](https://scrapbox.io/villagepump/2022/03/25)
<img src='https://scrapbox.io/api/pages/villagepump/nishio/icon' alt='/villagepump/nishio.icon' height="19.5"/>
- Watchlist、どうやって追加するのか良くわからないなぁと思いながら放置してたんだけどもしかして他の人は自動的に追加されてるの？？
    - ![image](https://gyazo.com/1900d8686c0ba3730f12963b1048193e/thumb/1000)
        - 人のProject開いたら追加されますね<img src='https://scrapbox.io/api/pages/villagepump/kuuote/icon' alt='/villagepump/kuuote.icon' height="19.5"/><img src='https://scrapbox.io/api/pages/villagepump/blu3mo/icon' alt='/villagepump/blu3mo.icon' height="19.5"/><img src='https://scrapbox.io/api/pages/villagepump/takker/icon' alt='/villagepump/takker.icon' height="19.5"/>
            - ![image](https://gyazo.com/a861d978005cf61506061bf247ab31c2/thumb/1000)

            - されないとしたらバグ？
            - Porterだからかな？？<img src='https://scrapbox.io/api/pages/villagepump/nishio/icon' alt='/villagepump/nishio.icon' height="19.5"/>
                - ありそう<img src='https://scrapbox.io/api/pages/villagepump/kuuote/icon' alt='/villagepump/kuuote.icon' height="19.5"/>
            - localStorageとかに入れてるんだと思うけどなんかうまいことPorterでも追加できないかなぁ<img src='https://scrapbox.io/api/pages/villagepump/nishio/icon' alt='/villagepump/nishio.icon' height="19.5"/>
                - 自動でなくても手動でもいいんだけど。
            - UserScriptで追加できます<img src='https://scrapbox.io/api/pages/villagepump/takker/icon' alt='/villagepump/takker.icon' height="19.5"/>
                - 例えば[/takker/remote watch list#61c291b71280f00000f6d645](https://scrapbox.io/takker/remote watch list#61c291b71280f00000f6d645)を使うと、`list.js`にある約1000個のprojectsがwatch listに追加されます
                    - あ、`list.js`にはprivate projectも含まれていたんだった
                        - たぶん知ってるもの数個だけを入れて試してみるので大丈夫<img src='https://scrapbox.io/api/pages/villagepump/nishio/icon' alt='/villagepump/nishio.icon' height="19.5"/>


[/takker/remote watch list](https://scrapbox.io/takker/remote watch list)

script.js

```javascript
const projectIds = [
'5e6cbe2d71038b00178729b1', // /sta stakiran研究所
'5ad2d6b60268550014c2d723', // /rashitamemo 倉下忠憲の発想工房
'57ba889cc59c3e0f00979915', // /shokai 橋本商会
'60d84407e00111001ca49f7b', // /blu3mo-public bluemo-public
'5ad25639fcbd1b0014f970fb', // /dai-yamamoto dai-yamamoto
'5844e6b756624e0011d8e6c2', // /daiiz daiiz
'5b2b0eebb7bd41001461d2f4', // /halsk Hal Seki (関 治之)の Scrapbox
'5f260ed82c98a7001eddd442', // /issac-37765679 issacのScrapbox
'5886ce9301cee80011d205a8', // /june29 29box
'58c9deee4dd2070011214160', // /kimiyuki 未来の自分が読むメモ
'583dc452ebcbae0011e236ce', // /masui 増井俊之
'59fb21121207900012774b18', // /motoso 基素基
'5ae7fecf7766b7001455cbd4', // /mtane0412 汲取式思考便所
'5f1810a1592883001eacf6b4', // /noratetsu Noratetsu's Room（のらてつ研究所）
'5c6f5ba148eb0400174a245a', // /nwtgck nwtgck / Ryo Ota
'5f2f02f3c4a48d00237e1534', // /takker くたくたじゅうよん
'60648a9d02a598001c91685e', // /takoeight0821 星にゃーんのScrapbox
'5b6cd7c5e5da53001413f00e', // /taskmanagement タスク管理のScrapbox
'5f112854fd61a2001e36f78e', // /tkgshn tkgshn
'5983f25ce54f440011c2cd40', // /yamanoku yamaScrapbox
'60296e715a38ec001c5f1909', // /yosider yosider
'6016a310e41b6a0021bd81fa', // /hanadev
'5b8aa7cc1a07780014f61b7a', // /sudow
]
```


/hanadev
/sudow
- リストにないプロジェクトを追加したかったらIDをどうやって調べたらいいですか？
    - [/scrapboxlab/api/projects/:projectname](https://scrapbox.io/scrapboxlab/api/projects/:projectname)を使います<img src='https://scrapbox.io/api/pages/villagepump/takker/icon' alt='/villagepump/takker.icon' height="19.5"/>

script.js

```javascript
function syncWatchList(projectIds) {
  // 既存のwatchListは上書きしない
  const projectsLastAccessed = JSON.parse(localStorage.getItem('projectsLastAccessed'));
  projectIds.forEach(id => projectsLastAccessed[id] ??= 0);
  localStorage.setItem('projectsLastAccessed', JSON.stringify(projectsLastAccessed));
}
syncWatchList(projectIds);
console.log("add watchlist")
```


- ダメだった
    - Porter内のブラウザにlocalStorageがないとかなのかなー
