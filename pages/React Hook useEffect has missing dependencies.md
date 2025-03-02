
ts

```typescript
  const [state, setState] = useGlobal("state");
  const { key } = useParams();
  useEffect(() => {
    if (state === "NORMAL") {
      if (key === "new") {
        foobar().then((id) => {
          setState("CREATED_NEW")
        });
        setState("WAIT_NEW")
      }
    }  // (snip)
  }, [key]) 
```

keyの変化をトリガーにしてstateを更新したいという意図でこう書いたのだが、stateに対してmissing dependenciesだと警告される
何がいけないのか、どうするのがいいのか
