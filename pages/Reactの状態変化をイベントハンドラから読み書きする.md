
2019-05-17 [[React勉強日記]]
「1秒ごとに変更されてるかチェックして変更されていたら保存する」という実装をしようとして、Reactの関数コンポーネントの中でsetIntervalでチェックするコードを書いたが、これは正しくない。
typescript

```typescript
const App: React.FC = () => {
  let [toSave, setToSave] = useState(false);
  
  useEffect(() => {
    let t = setInterval(() => {
      if (toSave) {                    // NG
        setToSave(false);
        // saveSomething()
      }
    }, 1000)
  }, []);
```


なぜかというと、setIntervalの引数に渡されている関数オブジェクト(以下fと呼ぶ)の中のtoSaveは、fが作成されたタイミングでの外のスコープにあるtoSaveを指していて、その後のsetToSaveの呼び出しなどで状態が更新されても、ずっと初期値のfalseのままだから。

この件に関して「状態をmutableなオブジェクトにして破壊的に更新する」という案があった。
これはまた別の罠を踏む。

このコードでは2つのタイマーが1つの状態を片方(1)は定期的に読み、もう片方(2)は定期的に書き換えている。その2つの表示は順次カウントアップしていくので期待通りに動いているように見えるかもしれない。だが(3)のDOMの更新はされない。
typescript

```typescript
const App: React.FC = () => {
  let [count, setCount] = useState({value: 0});

  useEffect(() => {
    let t = setInterval(() => {
      console.log("Read Timer", count);  // (1)
    }, 1000)
  }, []);

  useEffect(() => {
    let t = setInterval(() => {
      count.value++;
      setCount(count);
      console.log("Write Timer", count);  // (2)
    }, 1000)
  }, []);

  return (
    <div>
      <p>You clicked {count.value} times</p>    // (3)
    </div>
  );
}
```

僕も昨日まで知らなかったが、過去の値を破壊的に書き換えてそれをsetCountに渡した場合、setCountは「変化してない」と判断してしまう。なのでDOMの更新がトリガーされない。

> Both useState and useReducer Hooks bail out of updates if the next value is the same as the previous one. Mutating state in place and calling setState will not cause a re-render.
- [https://reactjs.org/docs/hooks-faq.html#is-there-something-like-forceupdate](https://reactjs.org/docs/hooks-faq.html#is-there-something-like-forceupdate)

つまりこのサンプルコードでWrite Timerが書いた値をRead Timerが読めてるように見えるのは、Reactの状態管理の効果ではなく「両方が同一のオブジェクトを読み書きしているから」だ。下記のようにuseStateを使うのをやめても同じ振る舞いをする。
typescript

```typescript
const App: React.FC = () => {
  // 書き換え
  // let [count, setCount] = useState({value: 0});
  let count = {value: 0};
  ...
  useEffect(() => {
    let t = setInterval(() => {
      count.value++;
      // コメントアウト
      // setCount(count);
      console.log("Write Timer", count);
    }, 1000)
  }, []);
...
```


Write Timerで、新しいオブジェクトを作ってsetCountするようにすると、1回re-renderがトリガーされる。しかし2つのタイマーのcountが指している値は初回render時のスコープにある{value: 0}のままなので、カウントアップされていくことはない。

で、どうするのがよいのか、はまだよくわかってない。[[useRef]]?

----
2019-05-18
useRefはre-renderをトリガーしないので、useStateと一緒に使って、3ヶ所全部が更新されるようになった。
typescript

```typescript
const App: React.FC = () => {
  let [count, setCount] = useState({value: 0});
  let countRef = useRef(count);
  
  useEffect(() => {
    let t = setInterval(() => {
      console.log("Read Timer", countRef.current);
    }, 1000)
  }, []);

  useEffect(() => {
    let t = setInterval(() => {
      let newCount = {value: countRef.current.value + 1};
      setCount(newCount);
      countRef.current = newCount;
      console.log("Write Timer", newCount);
    }, 1000)
  }, []);

  return (
    <div>
      <p>You clicked {count.value} times</p>
    </div>
  );
}
```


