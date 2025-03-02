---
title: "React Hooksでgetter"
---

こういうの作ったらどうだろう。(思いつきなのでまだしっかり検証していない)
typescript

```typescript
function useGetter<T>(init_value : T){
  let [state, update] = useState<T>(init_value);
  let ref = useRef(state);
  const getter = () => {
    return ref.current;
  }
  const setter = (f : Function) => {
    let newState = f(ref.current);
    newState = Object.assign({}, newState);  // force update
    ref.current = newState;
    update(newState);
  }
  return [getter, setter];
}
```

[[React Hooks]]
[[React]]
