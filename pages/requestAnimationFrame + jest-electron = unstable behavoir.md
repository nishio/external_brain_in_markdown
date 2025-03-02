---
title: "requestAnimationFrame + jest-electron = unstable behavoir"
---

`requestAnimationFrame` + `jest-electron` causes unstable behavoir includes crush of elecron.
To replace `requestAnimationFrame` with `setTimeout` solves the problem for now.

solution
ts

```typescript
beforeEach(() => {
  jest.spyOn(window, "requestAnimationFrame").mockImplementation(callback => {
    return setTimeout(callback, 0);
  });
});

afterEach(() => {
  window.requestAnimationFrame.mockRestore();
});
```



-----
- OK
ts

```typescript
test("promise", async () => {
  let _resolve: (arg: unknown) => void;
  const p = new Promise(res => {
    _resolve = res;
  }).then(() => {
    console.log("resolved");
  });
  _resolve!(0);
  await p;
});
```

- resolved / `Timeout - Async callback was not invoked within the 5000`
ts

```typescript
test("promise", async () => {
  let _resolve: (arg: unknown) => void;
  const p = new Promise(res => {
    _resolve = res;
  }).then(() => {
    console.log("resolved");
  });
  requestAnimationFrame(() => {
    _resolve!(0);
  });
  await p;
});
```

- OK
ts

```typescript
test("promise", async () => {
  let _resolve: (arg: unknown) => void;
  const p = new Promise(res => {
    _resolve = res;
  }).then(() => {
    console.log("resolved");
  });
  requestAnimationFrame(() => {
    _resolve!(0);
  });
  await p;
  console.log("ok");
});
```

- resolved / Timeout
ts

```typescript
test("promise", async () => {
  let _resolve: (arg: unknown) => void;
  const p = new Promise(res => {
    _resolve = res;
  }).then(() => {
    console.log("resolved");
  });
  requestAnimationFrame(() => {
    _resolve!(0);
  });
  await p;
  expect(1).toBe(1);
});
```


- Unstable Behavoir: Fails as expected, crush, or Timeout
ts

```typescript
test("promise", async () => {
  let _resolve: (arg: unknown) => void;
  const p = new Promise(res => {
    _resolve = res;
  }).then(() => {
    console.log("resolved");
  });
  requestAnimationFrame(() => {
    _resolve!(0);
  });
  await p;
  expect(1).toBe(0);
});
```

    - ![image](https://gyazo.com/47e1e651a4c2e60de8a19a2cb62d3914/thumb/1000)
    - Timeout
        - ![image](https://gyazo.com/cac5a7eb56b179ee58794b7c2f4c2490/thumb/1000)

change requestAnimationFrame to setTimeout
- OK
ts

```typescript
test("promise", async () => {
  let _resolve: (arg: unknown) => void;
  const p = new Promise(res => {
    _resolve = res;
  }).then(() => {
    console.log("resolved");
  });
  setTimeout(() => {
    _resolve!(0);
  });
  await p;
});
```

- OK
ts

```typescript
test("promise", async () => {
  let _resolve: (arg: unknown) => void;
  const p = new Promise(res => {
    _resolve = res;
  }).then(() => {
    console.log("resolved");
  });
  setTimeout(() => {
    _resolve!(0);
  });
  await p;
  expect(1).toBe(1);
});
```


solution
ts

```typescript
beforeEach(() => {
  jest.spyOn(window, "requestAnimationFrame").mockImplementation(callback => {
    return setTimeout(callback, 0);
  });
});

afterEach(() => {
  window.requestAnimationFrame.mockRestore();
});
```


