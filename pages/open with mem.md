
![image](https://gyazo.com/3bbaf1713975f9e25a0e9c43a9ec08f3/thumb/1000)

script.js

```javascript
const onClick = () => {
  location.href = location.href.replace('scrapbox.io/nishio','mem.nhiro.org');
};

scrapbox.PageMenu.addMenu({
  title: "mem",
  image: "https://gyazo.com/3bbaf1713975f9e25a0e9c43a9ec08f3/raw",
  onClick,
});
```

