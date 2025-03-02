
[[ReactNを露出する]]して[[Cypress]]からsetGlobalを使ってテスト用の状態を作り、それをテストする。

できた。
![image](https://gyazo.com/4555d5f590786e4b4d2a4982ddf31aec/thumb/1000)

App.tsx

```
function App() {
  const [fusens] = useGlobal("fusens");
  return (...);
}
```


index.tsx

```
setGlobal(INITIAL_GLOBAL_STATE);
const movidea = {
  getGlobal,
  setGlobal,
};

const debug = {};

declare global {
  interface Window {
    debug: any;
    movidea: typeof movidea;
  }
}

window.movidea = movidea;
window.debug = debug;
```

解説は[[ReactNを露出する]]
- 僕はアプリの公開時にもユーザ(主に僕)がハックしやすいようにmovidea(アプリ名)にsetGlobalなどをつけてるけど、debugの方につけてリリースビルドでは削るって設計もアリだと思う。

テストコード
cypress/.../adjust_font_size.js

```javascript
/// <reference types="cypress" />

describe('adjust font size', () => {
  beforeEach(() => {
    cy.visit('/')
    let a = 1;
    let b = 1;
    const fusens = [];
    for (let i = 0; i < 11; i++) {
      [a, b] = [b, a + b];
      fusens.push({
        text: ">" + "あ".repeat(a),
        x: 50 * i,
        y: 50 * i,
      });
    }
    cy.window().its('movidea').then(movidea => {
      setTimeout(() => {
        movidea.setGlobal({ fusens });        
      })
    });
  })

  it('fusen sizes', () => {
    cy.get('.fusen').should('have.length', 12).first()
      .should("have.css", "font-size", "66px")
      .should("not.have.css", "align-items", "flex-start")
    cy.get('.fusen').eq(1).should("have.css", "font-size", "53px")
    cy.get('.fusen').eq(2).should("have.css", "font-size", "38px")
    cy.get('.fusen').eq(10)
      .should("have.css", "font-size", "10px")
      .should("have.css", "align-items", "flex-start")
  })
})
```

setTimeoutに関しては see [[✅CypressからsetGlobalするとフックが反応しない]]

