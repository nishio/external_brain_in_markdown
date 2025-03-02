
from [[Jestメモ]]
Jestメモ Day3
--- day 3
- `MissingAPIError: indexedDB API missing`
    - Firestoreの時と同様にIndexeDBに触れるコードも分離してモックで置き換える必要がある
    - 前回、Firestoreから値を取った後のコードを下記のように切り出してエクスポートし、これを直接呼び出すPromiseでgetNewTalkIDを置き換える、というモックをした
ts

```typescript
// exported for test
export const _gotNewTalkID = (text: string) => {
  return localDB.talks
    .orderBy("id")
    .reverse()
    .limit(1)
    .toArray()
    .then((x) => {
      const previousTalkID = x[0]?.TalkID;
      if (previousTalkID !== undefined) {
        setGlobal({ TalkID: text, previousTalkID: x[0].TalkID });
      } else {
        setGlobal({ TalkID: text, previousTalkID: "" });
      }
      localDB.talks.add({ TalkID: text });
    });
};
```

- Promiseの型を明記しつつ読み出し、利用、書き込みの3つの関数に分割
- [[Jestのモックは同一モジュール内の呼び出しに影響を与えない]]から、IndexedDBに触れるところだけ別モジュールにくくり出してモックしよう
- ユーザーモジュールのモック [doc](https://jestjs.io/docs/ja/manual-mocks#%E3%83%A6%E3%83%BC%E3%82%B6%E3%83%BC%E3%83%A2%E3%82%B8%E3%83%A5%E3%83%BC%E3%83%AB%E3%81%AE%E3%83%A2%E3%83%83%E3%82%AF)
    - なるほど
    - でも2通りの実装が欲しいな
__mocks__/managePreviousTalkID.ts

```typescript
// no previoud id
export const getPreviousTalkID = (): Promise<string> => {
  return Promise.resolve("");
};
export const MOCK_PREVIOUS_ID_EXISTS = (): Promise<string> => {
  return Promise.resolve("test");
};

export const updatePreviousTalkID = (currentTalkID: string): void => {};
```

- トップ画面の描画テストは動くようになった
    - jest.mockをテストケースの中ではなくトップレベルに置かないと期待通りにモックされない、なぜ？
    - 複数のモックの挙動を切り替えてテストしたいのだが…
- > jest.mockをテストケースの中ではなくトップレベルに置かないと期待通りにモックされない、なぜ？
    - > [docs](https://jestjs.io/docs/ja/manual-mocks#es-module-import%E3%82%92%E5%88%A9%E7%94%A8%E3%81%99%E3%82%8B): ES module importsを使用している場合、通常はテストファイルの先頭でimport宣言を書くことが多いでしょう。 しかしモジュールがそれらを使用するのに先立ち、Jestにモックを使用するよう指示する必要があります。 このため、Jestは自動的にjest.mockコールを自動的にモジュールの先頭に(importを行う前に)移動します。
    - 「先におかないといけないのでは？」と思ったがESLintが "Import in body of module; reorder to top." と文句を言うので後に置いてた。
    - 後においても動くのでmockのタイミングでインポート済みのものを置き換えるのかなと思ってたがそういうことではないようだ。
- spyOnなら確実にそのタイミングでの差し替えを行うので、重ねてspyOnすることにしてみた
    - previousTalkIDが存在するかどうかでメニューの表示が異なる、というテストが一応動いた
    - しかし(1)の部分、メニューが実際に存在しないのか、まだ非同期の再描画が終わってないのか判断がつかないと思う
        - タイムアウトするまで待てば判断つくけど、テストが遅くなるから嫌だし
ts

```typescript
  const { container } = render(<App />);
  expect(container).toMatchSnapshot();
  fireEvent.click(screen.getByLabelText("menu"));
  expect(screen.queryByText("Re-enter to Last Talk")).toBeNull();  // (1)

  jest
    .spyOn(managePreviousTalkIDModule, "getPreviousTalkID")
    .mockResolvedValue("test");
  render(<App />);
  await waitFor(() => screen.getByText("Re-enter to Last Talk"));

  expect(screen.queryByText("Re-enter to Last Talk")).not.toBeNull();
```


![image](https://gyazo.com/84b751a483459c1c05459b425c3d973e/thumb/1000)

[[Reactのテストでactで包むのはrenderではなく状態更新]]
[[Promiseの結果で状態更新する場合、全体をactで包んでもダメ]]

次回「useStateをモックで置き換えたらいいのでは？」
