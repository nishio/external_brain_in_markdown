
[/porterapp/SafariのScrapboxのページからPorterへスイッチ(Switch from Safari to Porter)](https://scrapbox.io/porterapp/SafariのScrapboxのページからPorterへスイッチ(Switch from Safari to Porter))
をPage Menuから呼ぶ

![image](https://gyazo.com/d4c84afa1b488a1b4766ae6aa1295a9f/thumb/1000)

script.js

```javascript
const onClick = () => {
  location.href = location.href.replace('https','sbporter');
};

scrapbox.PageMenu.addMenu({
  title: "Porter",
  image: "https://gyazo.com/d4c84afa1b488a1b4766ae6aa1295a9f/raw",
  onClick,
});
```


