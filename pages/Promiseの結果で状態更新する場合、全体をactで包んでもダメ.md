---
title: "Promiseの結果で状態更新する場合、全体をactで包んでもダメ"
---

前提の話、[[Reactのテストでactで包むのはrenderではなく状態更新]]を踏まえて、ではこの状態更新が非同期の時にはどうなるのか、という話。

前回はテストコードの中でsetValueを直接呼んだが、今回は`asyncUpdate`というPromiseのthenで呼ぶ形にする。
例えばネットワークアクセスをした結果や、IndexedDBの読み出し結果などはPromiseの形になってることが多い。テストの際にモックで置き換えたとしてもPromiseであることは変わらないので、こういう形での非同期な状態更新が行われる。

これはテストに失敗する。
test.tsx

```
test("MyComponent2", async () => {
  type TSetState = React.Dispatch<React.SetStateAction<number>>;
  let setValue: TSetState | undefined;
  const exportSetValue = (s: TSetState) => {
    setValue = s;
  };
  const asyncUpdate: Promise<number> = new Promise((resolve) => {
    resolve(1);
  });

  render(<MyComponent exportSetValue={exportSetValue} />);
  expect(screen.getByText("0")).toBeTruthy();
  expect(setValue).toBeTruthy();
  act(() => {
    asyncUpdate.then((x) => setValue!(x));
  });
  expect(screen.queryByText("0")).toBeNull(); // fails
  expect(screen.getByText("1")).toBeTruthy();
});
```


そして、前回`act`でラップしなかった時に出た警告 `Warning: An update to MyComponent inside a test was not wrapped in act(...).` がまた出る。
ラップしてるじゃん？何を言ってるのか？と思いそうになるが、つまりこのコードでは適切にラップできてないというのが問題の本質。

Promiseの振る舞いについておさらい。
[Promise - JavaScript | MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Promise)
- > プロミスは非同期であることが保証されていることに注意してください。したがって、既に「解決済み」のプロミスに対するアクションは、スタックがクリアされ、クロックティックが経過した後にのみ実行されます。この効果は setTimeout(action,10) とよく似ています

つまり下記のコードの`console.log`の順番の通り、`setValue`は`act`の外で呼ばれる。
ts

```typescript
console.log(1);
act(() => {
  console.log(2);
  asyncUpdate.then((x) => {
    console.log(5);
    setValue!(x);
  });
  console.log(3);
});
console.log(4);
expect(screen.queryByText("0")).toBeNull(); // fails
```


ならばどうすれば良いかというと、`setValue`を直接`act`でラップして、`await asyncUpdate.then`する。これで警告なくテストが通る。
test.tsx

```
test("MyComponent3", async () => {
  ...
  await asyncUpdate.then((x) => {
    act(() => {
      setValue!(x);
    });
  });
  expect(screen.queryByText("0")).toBeNull(); // OK
  expect(screen.getByText("1")).toBeTruthy();
});
```


この`await`を見て「あれ？actにawaitつけたらどうなるんだろ？」と試してみたら「actはプロミスを返さないのでawaitするな」と親切な警告が出た。
ts

```typescript
  await act(() => {
    asyncUpdate.then((x) => setValue!(x));
  });
```

warning

```
Warning: Do not await the result of calling act(...) with sync logic, it is not a Promise.
```


なおasync / awaitを使わない素朴な書き方もできる。ロジックは同じ。
Jest doc:[Promises](https://jestjs.io/docs/ja/asynchronous#promises) [Async/Await](https://jestjs.io/docs/ja/asynchronous#asyncawait)
- > これらのケースでは async や await は事実上、promiseを使用した例と同じロジックの糖衣構文です。

test.tsx

```
test("MyComponent4", () => {
  ...
  return asyncUpdate
    .then((x) => {
      act(() => {
        setValue!(x);
      });
    })
    .then(() => {
      expect(screen.queryByText("0")).toBeNull(); // OK
      expect(screen.getByText("1")).toBeTruthy();
    });
});
```


さて、`Promise`によって非同期に`setValue`される場合にどうすべきであるのか、原理のところは理解できた。
次に解決するべき問題は？
「ユーザがボタンをクリックしたら、ネットワークアクセスをして結果を表示」というシナリオを考えてみると、Promiseが`setValue`するコードはテストコードの中ではなく本体コードの側で一塊のイベントハンドラになってる場合が多い。
この本体コードに手を入れて`setValue`を`act`で包むのは現実的ではない。
さあどうするか？というところで続きは次回。
ts

```typescript
test("MyComponent5", async () => {
  ...
  const userEventHandler = () => {
    asyncUpdate.then((x) => {
      setValue!(x);
    });
  };

  render(<MyComponent exportSetValue={exportSetValue} />);
  expect(screen.getByText("0")).toBeTruthy();
  expect(setValue).toBeTruthy();

  userEventHandler(); // Here
  expect(screen.queryByText("0")).toBeNull(); // fails
  expect(screen.getByText("1")).toBeTruthy();
});
```


[[非同期なReactの状態更新をテストする]]
