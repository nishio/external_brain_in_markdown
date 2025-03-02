
Deno 1.20.4

```
> JSON.parse({})
Uncaught SyntaxError: Unexpected token o in JSON at position 1
    at JSON.parse (<anonymous>)
```


既にJSON.parseされているのに、間違えてもう一度JSON.parseして発生した
- ([[Next.js]]でreq.bodyに文字列が入っていると思い込んでJSON.parseしたが、親切にもすでにparseされてるので必要なかった)

なぜ「token o」かというと暗黙にtoStringされてるから
Deno 1.20.4

```
> {}.toString()
"[object Object]"
```


Chrome上だともう少しわかりやすいエラーになる
Chrome 105.0.5195.102

```
JSON.parse({})
VM366:1 Uncaught SyntaxError: "[object Object]" is not valid JSON
    at JSON.parse (<anonymous>)
    at <anonymous>:1:6
```

