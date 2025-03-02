---
title: "refとuseEffect"
---

![image](https://gyazo.com/9a294a69bcfc79a07aa38d51b4722ef8/thumb/1000)

- 2段目はDOMの生成。関数コンポーネントの関数の実行が終わった後で行われる。useEffectはそれが終わった後で呼ばれる。

ts

```typescript
const MyComponent: React.FC<{}> = () => {
  console.log("function body")
  const [, setX] = useState({});
  const ref = useRef(null);
  console.log("ref.current", ref.current);
  useEffect(() => {
    console.log("useEffect")
  })
  const onClick = () => {
    console.log("onClick");
    setX({});
  }
  return <div ref={ref}>
    <button onClick={onClick}>redraw!</button>
  </div>
}
```

![image](https://gyazo.com/919b4dfb1d3b951bb6fd1b6deff2d55d/thumb/1000)

