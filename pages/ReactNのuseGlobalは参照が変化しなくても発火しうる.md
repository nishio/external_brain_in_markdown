
下に「ボタンを押すとyの値が変わるコード」がある。
コンポーネントComp1は`useGlobal("x")`しているのでxが変わった時だけ再描画されることを期待している。
しかし、意外なコードで期待していない再描画が起きたのでメモする。

ts

```typescript
const TestApp = () => {
  console.log("render TestApp");
  return (
    <div>
      <Comp1 />
      <Comp2 />
    </div>
  );
};
const Comp1 = () => {
  const [x] = useGlobal("x");
  console.log("render Comp1");
  return <span>{x}</span>;
};
const Comp2 = () => {
  const onClick = () => {
    console.log("onClick");
    // !!HERE!!
  };
  return <button onClick={onClick}>update y</button>;
};

```


ts

```typescript
// NG: 再描画される
setGlobal((currentState) => ({ ...currentState, y: "hello" }));
// NG: 何も更新してないのに再描画される
const currentState = getGlobal();
setGlobal(currentState);
// OK
setGlobal({y: "hello"});
```

つまり、たとえ同じ参照がsetされるとしても更新があったと判定してしまう。
- [https://github.com/CharlesStover/reactn/blob/f4eb2fc4a3c616a7d0b6a0ff2c0f299784dc5826/src/global-state-manager.ts#L196](https://github.com/CharlesStover/reactn/blob/f4eb2fc4a3c616a7d0b6a0ff2c0f299784dc5826/src/global-state-manager.ts#L196)

前者の書き方なんかしないだろと思うかもしれない(この例だと必要ないから)
Stateが複雑な場合にimmerで更新しようとしてこの問題を踏んだ。これはState全体を受け取り、更新したいものだけを更新したオブジェクトを作って返す。なので更新されない値も保持した`{ ...currentState, y: "hello" }`に相当するものができてしまう。

[[変更差分を作ってsetGlobalする]]
