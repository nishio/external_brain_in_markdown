
- ブックマークレットは、プログラミングに入門する良い機会
    - 「ちょっと書いたら日々の作業が楽になる」
- しかし制約が厳しいせいで見た目がわかりにくい、余計な認知的負担
    - 1行にしなければいけない
    - URLエンコードしなければならない
- Scrapboxを使うときれいな見た目のままブックマークレットにできる
    - Scrapboxはページ内のソースコードを返すAPIを持っている
        - `https://scrapbox.io/nishio/test_alert`に書かれたソースコードが`https://scrapbox.io/api/code/nishio/test_alert/script.js`で得られる
        - このURLをsrcとするscriptタグをbodyに追加するブックマークレットを作る

指定URLをsrcとするscriptタグをbodyに追加するコード
:

```
var url="https://scrapbox.io/api/code/nishio/test_alert/script.js";
var elm=document.createElement('script');
elm.setAttribute('src', url);
document.body.appendChild(elm);
```

それをブックマークレットにしたもの
:

```
javascript: var url="https://scrapbox.io/api/code/nishio/test_alert/script.js"; var elm=document.createElement('script');elm.setAttribute('src', url);document.body.appendChild(elm); 
```


メリット
- 修正と実験のサイクルを高速に回すことができる
    - コードを読みやすい形に保ったまま修正できる
    - 1行にしたりする手間がいらない
    - ブックマークレットを編集する作業がいらない。
        - 参照先のスクリプトが変わるから。
        - ブックマークレット自体は「この場所のスクリプトを読め」という命令で、それは変わらないから。
    - エラーの場所がわかりやすい
        - ![image](https://gyazo.com/5bbf9072ea1c401a0e518318d696bab4/thumb/1000)


デメリット
- 一部のサービスがこのタイプのブックマークレットを受け付けない
    - Facebook
    - Content Security Policyでスクリプト読み込みに制限をかけていて、そのホワイトリストにScrapboxが含まれていない
    - `Refused to load the script 'https://scrapbox.io/api/code/nishio/test_alert/script.js' because it violates the following Content Security Policy directive: "script-src *.facebook.com *.fbcdn.net *.facebook.net *.google-analytics.com *.virtualearth.net *.google.com 127.0.0.1:* *.spotilocal.com:* 'unsafe-inline' 'unsafe-eval' *.atlassolutions.com blob: data: 'self'".`
    - Flickrも同様
    - `Refused to load the script 'https://scrapbox.io/api/code/nishio/test_alert/script.js' because it violates the following Content Security Policy directive: "script-src 'unsafe-eval' 'unsafe-inline' 'nonce-bace3aa55f7817dc19e2c90e7f842c1e' https://*.flickr.com https://s.yimg.com https://cdn.yahooapis.com https://yui-s.yahooapis.com https://de.adserver.yahoo.com https://fc.yahoo.com https://radar.cedexis.com https://*.braintreegateway.com https://*.sandbox.paypal.com https://*.paypal.com https://*.paypalobjects.com".`
    - どちらのケースもunsafe-evalはついているから、xhrで取ってからevalするブックマークレットを作ればよいか？？
        - xhrでGETする部分で同様にはじかれてしまう
:

```
var url = "https://scrapbox.io/api/code/nishio/test_alert/script.js";
var oReq = new XMLHttpRequest();
oReq.addEventListener("load", (x)=>{eval(x.target.response));
oReq.open("GET", url);
oReq.send();
```

            - `javascript: var url = "https://scrapbox.io/api/code/nishio/test_alert/script.js";var oReq = new XMLHttpRequest();oReq.addEventListener("load", (x)=>{eval(x.target.response)});oReq.open("GET", url);oReq.send();`

