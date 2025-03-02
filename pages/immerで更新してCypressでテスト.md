
[[ReactNを露出してCypressから使う]]ができたので、
状態を[[immer]]で更新して[[Cypress]]でテストしてみる

できた
test.js

```javascript
cy.contains("DEF").should("have.css", "width", "260px");
cy.window()
  .its("movidea")
  .then((movidea) => {
    movidea.updateGlobal((g) => {
      g.itemStore["3"].scale = 3;
    });
  });
cy.contains("DEF").should("have.css", "width", "390px");
```

![image](https://gyazo.com/52722b57be6389fc6ebef2b0825a6cd0/thumb/1000)

ところでテストコードはデフォルトのJSなのだが、これだとupdateGlobalのgがanyになってしまう。
補完が効かないからいずれTypoしそうだな…と思ったらさっそくTypoして「位置を更新したのに位置が変わらない、位置の値を描画時に読んでないのか？あれ位置が更新されてないぞ？」とかやってしまった
![image](https://gyazo.com/aa50d968a68da1936e93ddd738262053/thumb/1000)

つづき [[CypressのTypeScript化]]