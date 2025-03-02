


script.js

```javascript
scrapbox.PopupMenu.addButton({
  title: "GPT",
  onClick: (text) => {
    console.log(text)
    const name = /NISHIO Hirokazu\n/g;
    const my_icon = "[nishio.icon]";
    const ai_icon = "[gpt.icon]";
    let result = "";
    let indent = 0;
    for (let line of text.replace(name, my_icon).split("\n")) {
      if (line === "") continue;
      if (line.startsWith(my_icon)) {
        result += line + "\n";
        indent = 0;
      } else if (indent === 0) {
        result += ai_icon + line + "\n";
        indent = 1;
      } else {
        result += " ".repeat(indent) + line + "\n";
      }
    }
    return result;
  },
});
```


