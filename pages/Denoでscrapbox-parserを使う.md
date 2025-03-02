
[[Deno]] [[scrabox-parser]]
hello.ts

```typescript
import { parse } from "https://deno.land/x/scrapbox_parser@0.0.1/src/index.ts";
console.log(parse("\nhello[a link]world"));
```

output

```
$ deno run hello.ts
Check file:///Users/nishio/scaffold_network/hello.ts
[
  { type: "title", text: "" },
  {
    indent: 0,
    type: "line",
    nodes: [
      { type: "plain", raw: "hello", text: "hello" },
      { type: "link", raw: "[a link]", pathType: "relative", href: "a link", content: "" },
      { type: "plain", raw: "world", text: "world" }
    ]
  }
]
```


[/villagepump/2022/04/06#624d16c0aff09e00000d8e3d](https://scrapbox.io/villagepump/2022/04/06#624d16c0aff09e00000d8e3d)
