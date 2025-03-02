---
title: "Jestメモ Day2"
---

from [[Jestメモ]]
Jestメモ Day2
- テストユーティリティの謎の挙動
    - 結論: ReactTestUtilsを使うのをやめる
    - [テストユーティリティ – React](https://ja.reactjs.org/docs/test-utils.html)で[React Testing Library | Testing Library](https://testing-library.com/docs/react-testing-library/intro/)を使うのがおすすめされてるので従う
- とりあえずまずはコンポーネントをレンダリングして観察しようと思った
    - `await render(<ShowLog talk="SJSLzd0PCLcJ3Nzlfdc4" />);`
:

```
(node:40175) UnhandledPromiseRejectionWarning: Error: FIRESTORE (7.24.0) INTERNAL ASSERTION FAILED: Unexpected state
(node:40175) UnhandledPromiseRejectionWarning: Unhandled promise rejection. This error originated either by throwing inside of an async function without a catch block, or by rejecting a promise which was not handled with .catch(). To terminate the node process on unhandled promise rejection, use the CLI flag `--unhandled-rejections=strict` (see https://nodejs.org/api/cli.html#cli_unhandled_rejections_mode). (rejection id: 36)
(node:40175) PromiseRejectionHandledWarning: Promise rejection was handled asynchronously (rejection id: 36)
```

    - うーん、どうやらawaitでFirestoreにアクセスするPromiseを呼ぶとエラーになるっぽい
    - 一方でawaitしないと、データを得る前に次のコードに処理が移ってしまう
    - 「データを読み込む→setGlobalする」というコードを2つに分けて、データを取り終わったところでPromiseを返すようにし、それのthenでexpectする [doc](https://jestjs.io/docs/en/asynchronous#promises)
ts

```typescript
test("show log", () => {
  return loadLogsFromFirestore("SJSLzd0PCLcJ3Nzlfdc4").then((talkObject) => {
    expect(talkObject).toMatchSnapshot();
  });
```

        - ダメだ、それでも `FIRESTORE (7.24.0) INTERNAL ASSERTION FAILED: Unexpected state`
    - テストコードのなかでFirestoreにアクセスするのをやめよう
        - Firestoreは自前でリトライをしたりとかするのでテストの中で触らない方が良さそう
    - アプリのトップレベルでFirestoreから取った値を表示する
ts

```typescript
function App() {
  const [logs, setLogs] = useState("");
  loadLogsFromFirestore("SJSLzd0PCLcJ3Nzlfdc4").then((talkObject) => {
    setLogs(JSON.stringify(talkObject));
  });
  return <pre>{logs}</pre>;
```

    - この内容をtalkObject.jsonに保存
        - `import * as MockTalkObject from "./talkObject.json";`で読める
    - Firestoreから読む関数をモックで置き換える
ts

```typescript
  const m = jest
    .spyOn(loadLogsModule, "loadLogsFromFirestore")
    .mockResolvedValue(MockTalkObject);
```

    - モックしてるのにエラーになる
        - これ同一モジュール内の関数呼び出しはモックしても置き換わらない風の挙動だな
            - 追加 [[Jestのモックは同一モジュール内の呼び出しに影響を与えない]]
        - モックする関数を独立のモジュールにしたら動いた
    - ここまで動いた
ts

```typescript
test("show log", () => {
  const m = jest
    .spyOn(loadLogsModule, "loadLogsFromFirestore")
    .mockResolvedValue(MockTalkObject);

  // no talkID needed beacuse loadLogsFromFirestore is mocked
  render(<ShowLog talk="" />);
  screen.debug();
});
```

    - しかしまだ目的のテストには辿り着かない
        - ReactのsetStateが非同期だからこれをやっても「データは受け取ったがまだ画面の再描画が行われてない状態」のDOMが得られる
    - rerenderか？ [doc](https://testing-library.com/docs/react-testing-library/api/#rerender)
ts

```typescript
  const { rerender } = render(<ShowLog talk="" />);
  rerender(<ShowLog talk="" />);
```

:

```
console.error
    Warning: An update to ShowLog inside a test was not wrapped in act(...).
    
    When testing, code that causes React state updates should be wrapped into act(...):
    
    act(() => {
      /* fire events that update state */
    });
    /* assert on the output */
    
    This ensures that you're testing the behavior the user would see in the browser. Learn more at https://reactjs.org/link/wrap-tests-with-act
```

    - いや、rerender以前にこのコードだけでも同じエラーメッセージが出るな。actで包めと言われたものを包んでるのにエラーになる
ts

```typescript
  act(() => {
    render(<ShowLog talk="" />);
  });
```

    - サンプルを読み直す [doc](https://testing-library.com/docs/react-testing-library/example-intro)
        - 特定のエレメントが出現するまで待ってるな
            - `await waitFor(() => screen.getByRole("heading"))`
            - これ再レンダリングが行われたかどうか知る方法がないから要素があるかの判定を何度も繰り返して待つ風の引数だな
        - しかし今回のテスト対象、ログのロード待ちなので特に新しく出現するエレメントがない
            - いやまてよ、ログデータはモックで固定されてるので、ログに出現する適当な文字列が出現するのを待てば良いのか
        - できた、debugでログがレンダリングされてるのを確認した
ts

```typescript
test("show log", async () => {
  const m = jest
    .spyOn(loadLogsModule, "loadLogsFromFirestore")
    .mockResolvedValue(MockTalkObject);

  // no talkID needed beacuse loadLogsFromFirestore is mocked
  render(<ShowLog talk="" />);
  await waitFor(() => screen.getByText("🙁"));
  screen.debug();
});
```

    - メニューからエクスポートを選んだ時にエクスポート内容として出力されるテキストをスナップショットする
ts

```typescript
const m2 = jest.spyOn(RegroupDialogModule, "openRegroupDialog");
fireEvent.click(screen.getByLabelText("menu"));
fireEvent.click(screen.getByText("Export for Regroup"));
expect(m2).toHaveBeenCalled();
expect(m2.mock.calls[0][0]).toMatchSnapshot();
```

        - `[0][0]`は初回呼び出しの1つ目の引数という意味
    - これは期待通りテストできた

- 昨日
    - ![image](https://gyazo.com/29e227d54e0659616f0efb73f7f60c1c/thumb/1000)
- 今日
    - ![image](https://gyazo.com/08401b0c38956da44c29a55d969cefa8/thumb/1000)
- めでたしめでたし

残り
![image](https://gyazo.com/2e99067085ced9ee46727cb443ad1fb5/thumb/1000)

あ、昨日のテストはフレームワークを変えるにあたってコメントアウトしたんだった。だからNewTalkのカバレッジが低いんだな。
次は昨日のテストを新しい方式で書き直すか。

--- matome
- ReactTestUtils [Test Utilities – React](https://reactjs.org/docs/test-utils.html#act)
    - > We recommend using React Testing Library
- React Testing Library:
    - > The @testing-library family of packages helps you test UI components in a user-centric way.  --- [doc](https://testing-library.com/docs/)
    - > The [[DOM Testing Library]] is a very light-weight solution for testing DOM nodes (whether simulated with JSDOM as provided by default with [[Jest]] or in the browser) [doc](https://testing-library.com/docs/dom-testing-library/intro/)
    - > [[React Testing Library]] builds on top of [[DOM Testing Library]] by adding APIs for working with React components. ... Projects created with [[Create React App]] have out of the box support for [[React Testing Library]] --- [doc](https://testing-library.com/docs/react-testing-library/intro)
    - [Example | Testing Library](https://testing-library.com/docs/react-testing-library/example-intro/)
    - [API | Testing Library](https://testing-library.com/docs/react-testing-library/api/#queries)
    - [About Queries | Testing Library](https://testing-library.com/docs/queries/about/)
- Jest
    - [The Jest Object · Jest](https://jestjs.io/docs/ja/jest-object)
    - [Testing React Apps · Jest](https://jestjs.io/docs/en/tutorial-react)
- [Promise - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)
