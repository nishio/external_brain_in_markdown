---
title: "Promise Quiz"
---

console.logがどの順で実行されるか答えよ
js

```javascript
const f = async () => {
  let resolve;
  const p = new Promise((r) => {
    resolve = r;
  });
  const p1 = p
    .then(() => {
      console.log("p1-1");
    })
    .then(() => {
      console.log("p1-2");
    });
  const p2 = p.then(() => {
    console.log("p2");
  });

  console.log("a");
  resolve();

  const p3 = p.then(() => {
    console.log("p3");
  });
  const p4 = p2
    .then(() => {
      console.log("p4-1");
    })
    .then(() => {
      console.log("p4-2");
    });
  console.log("b");
  await p;
  console.log("c");
  await p1;
  console.log("d");

  return Promise.all([p1, p2, p3, p4]);
};
f();
```


answer
answer

```
"a"
"b"
"p1-1"
"p2"
"p3"
"c"
"p1-2"
"p4-1"
"d"
"p4-2"
```

[https://jsfiddle.net/1bepvt28/](https://jsfiddle.net/1bepvt28/)
![image](https://gyazo.com/3d9124304768b8654495ca52e6015e13/thumb/1000)

解説
- ![image](https://gyazo.com/a76ac996f30b29fb5f758032178f0e24/thumb/1000)

- aの段階で、まだresolveされてないプロミスにチェーンしてるだけなので実行されない
- resolveした段階でpの直接の子である3つが実行キューに入る、キューに入るだけなのでまだ実行されない
- bが出力される
- await pで、このasync関数の同期的実行が終了する。続きの部分がキューに入る
- キューを空にする、先に入ってた3つを実行して、cが表示される
- この実行の際に2つがキューに入ってるので、次のawaitのタイミングでそれが表示される
