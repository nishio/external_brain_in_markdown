---
title: "CypressのTypeScript化"
---

テストコードをTSにするかJSにするかという話、とりあえずデフォルトのJSでやってたけど[[immerで更新してCypressでテスト]]で、型で補完が効かないせいで早速Typoしたので、やっぱり[[Cypress]]の[[TypeScript]]化は必須だという結論になった。

![image](https://gyazo.com/aa50d968a68da1936e93ddd738262053/thumb/1000)

[TypeScript | Cypress Documentation](https://docs.cypress.io/guides/tooling/typescript-support#Install-TypeScript)を参考にTypeScript化する。

下記のようなことを書いてある記述を見かけたがこれはcypressディレクトリの中にtsconfigを置く場合は適切ではない、そうでない場合もカスタムコマンドのことを無視してる
tsconfig.json

```json
"include": [
  "cypress/integration/*.ts",
  "cypress/integration/**/*.ts",
]
```

相対パスなのでこんな感じ(full)
tsconfig.json

```json
{
  "compilerOptions": {
    "target": "es5",
    "lib": [
      "es5",
      "dom"
    ],
    "types": [
      "cypress"
    ]
  },
  "include": [
    "*.ts",
    "**/*.ts",
    "../src/*.ts",
    "../src/**/*.ts",
  ]
}
```


*.tsxをインポートしようとすると--jsxが必要というエラーになるが、そもそも今回のユースケースでtsxをインポートできる必要があるか不明だったのでシンプルに保つことにした。

`import { State } from "reactn/default";`して型宣言をすればちゃんとTypoが警告されるようになった
![image](https://gyazo.com/cbbf38921672d36603034a047fa6e03c/thumb/1000)

ところで`@ts-ignore`してる件、
`cy.window().its("movidea").then((movidea) => { ... }` だと引数はanyで、
`cy.get("@movidea").then((movidea) => { ... }` だと `JQuery<HTMLElement>` になる。

いちいちmovideaをキャストするのは不便。
カスタムコマンドを作るか

ここでサンプルの通りにしたつもりで`Type 'Chainable' is not generic.`とか`Property 'movidea' does not exist on type 'cy & EventEmitter'.`とかになったりすったもんだがあったが最終的にこれでOK
cypress/support/index.ts

```typescript
/// <reference types="cypress" />
import { TMovidea } from "../../src/exposeGlobal";

declare global {
  namespace Cypress {
    interface Chainable {
      movidea(callback: (movidea: TMovidea) => void): Chainable;
    }
  }
}

Cypress.Commands.add("movidea", (callback: (movidea: TMovidea) => void) => {
  return cy.window().its("movidea").then(callback);
});
```


[公式ドキュメント](https://docs.cypress.io/guides/tooling/typescript-support#Types-for-custom-commands)に下記のように書いてあったんだけど、これエラーにならない？
ts

```typescript
declare namespace Cypress {
  interface Chainable {
    /**
     * Custom command to select DOM element by data-cy attribute.
     * @example cy.dataCy('greeting')
     */
    dataCy(value: string): Chainable<Element>
  }
}
```

Cypressのソースを確認したら
ts

```typescript
declare global {
  namespace Cypress {
    // TODO: Why is Subject unused?
    // eslint-disable-next-line @typescript-eslint/no-unused-vars
    interface Chainable<Subject = any> {
      ...
```

ってなってるので、globalを補ったら期待通りに動くようになった。

最終的にテストコード中でこう書けるようになった。破壊的に更新してるように見えるけどimmerを使って非破壊的更新がされてて、ちゃんとReactのフックによる再描画が走る。
test.ts

```typescript
    cy.movidea((movidea) => {
      movidea.updateGlobal((g) => {
        g.itemStore["1"].position = [100, 0];
      });
    });
```

