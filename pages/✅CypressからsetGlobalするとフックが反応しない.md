---
title: "✅CypressからsetGlobalするとフックが反応しない"
---

[[ReactNを露出する]]で、コンソールでsetGlobalして、コンポーネントの側のuseGlobalが変更を検知して再描画するところまでできた。
しかしsetGlobalを[[Cypress]]のテストコード内から呼び出すと、更新が検知されない。
- →setTimeoutを挟むことで解決した
- [[2021-07-15Movidea開発日記]] デフォルトでsetTimeoutしてたらテストケースを書くことがやりにくいケースが出てきたのでデフォルトは同期的に実行し、問題がある時だけ非同期にしようとしたら、全部同期的呼び出しでテストが通ってしまった、なぜだ
    - 「何もしてないのに直った！」
    - 問題が再現してから再検討する
- 2021-08-24　この件、全部同期的呼び出しにしたまま1ヶ月、特に問題が起こってない
    - Cypress側の更新でReactの扱いが改善したとかなのかな

解決編
これはiframeによってコンテキストが分かれてることとは無関係で、非同期周りの挙動だった

最小限のコードで解説する
まずシンプルなコンポーネント、useEffectでsetGlobalする(1)
App.tsx

```
function App() {
  const [fusens] = useGlobal("fusens");
  console.log("render");
  useEffect(() => {
    console.log("useEffect");
    window.movidea.callSetGlobal(); // (1)
  }, []);

  return (...);
}
```


この時、コンポーネントの本体が走った後、useEffectが走り、その中でsetGlobalされ、それを検知して再描画される
:

```
render
useEffect
call setGlobal
render
```


では(1)をコメントアウトし、テストケースの側でsetGlobalしたらどうなるか(2)
test.js

```javascript
describe('adjust font size', () => {
  beforeEach(() => {
    cy.visit('/')
    cy.window().its('movidea').then(movidea => {
      console.log("movidea resolved")
      movidea.callSetGlobal()  // (2)
    });
  })...
```


この時、初回の描画の後、useEffectが呼ばれるよりも前にsetGlobalが呼ばれ、この更新が検知されない
:

```
render
movidea resolved
call setGlobal
useEffect
```


この(2)の呼び出しにsetTimeoutを挟んで非同期にするとどうなるか(3)
test.js

```javascript
describe('adjust font size', () => {
  beforeEach(() => {
    cy.visit('/')
    cy.window().its('movidea').then(movidea => {
      console.log("movidea resolved")
      setTimeout(movidea.callSetGlobal, 0)  // (3)
    });
  })...
```


この場合はsetGlobalが呼ばれるのがuseEffectの後になり、期待通りに変更が検知され、再描画される
:

```
render
movidea resolved
useEffect
call setGlobal
render
```


というわけでワークアラウンドとしてはテストケースからの状態更新を非同期にすれば良いということになるが、微妙な解決策だなぁ

--- log
[Testing Redux Store](https://www.cypress.io/blog/2018/11/14/testing-redux-store/)
- Cypressのテスト画面からアプリのコンソールに入ってsetGlobalすれば画面は更新される
- しかしCypressのテストコードからこの解の記述のようにinvokeしても画面が更新されない
- 値の更新はエラーなく行われてgetGlobalしたらちゃんと値が入っている

ReactNでも明示的にストアを作成することに相当するこれをやってみたけど期待通りにいかない
[https://github.com/CharlesStover/reactn/blob/master/Provider.md](https://github.com/CharlesStover/reactn/blob/master/Provider.md)

わかったこと
- Cypressとテスト対象のアプリはそれぞれiframeで動いている
    - ![image](https://gyazo.com/e26319be12d0196b26f9a1590dff7e0e/thumb/1000)

わからないこと
- Providerを使わなかった場合、それぞれのframeがdefaultGlobalStateManagerを使う
    - これがframeごとに別れてしまうのかな？
    - シングルトンオブジェクトを作るためにはどこかにグローバルな存在が必要だから、windowに紐づいてそれを区別してるなら別のオブジェクトになりうる？
- そういう問題を解決するためにProviderがあるのでは？
    - 初期化時にGlobalStateManagerを作ってる
    - 他のframeでもそれが渡されるのだからそれを使うのでは？

うーむ、テストケースから状態をいじって表示をテストするってのができたらいいなと思ったのだが…
