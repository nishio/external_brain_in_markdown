
「Pomodoro」という文字列を選択してトマトメニューを押すと下記のような記法になる
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>🍅03:27-03:52 Pomodoro
[[ポモドーロテクニック]]で現在時刻と25分後の時刻を入れている

script.js

```javascript
scrapbox.PopupMenu.addButton({
  title: "🍅",
  onClick: (text) => {
    const name = "nishio";
    const timeFormat = (d) => {
      const h = d.getHours().toString().padStart(2, "0");
      const m = d.getMinutes().toString().padStart(2, "0");
      return `${h}:${m}`;
    }
    const now = new Date();
    const end = new Date(now.getTime() + (1000 * 60 * 25));
    return `[${name}.icon]🍅${timeFormat(now)}-${timeFormat(end)} [" ${text}]`;
  },
});
```


