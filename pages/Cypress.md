---
title: "Cypress"
---

ブラウザ上で動くテストフレームワーク
[[jest]]+[[jsdom]]でのテストと違って実際のブラウザを使うので、jsdomの実装による制限がない

まとめ:
- 同期非同期の区別は不要
    - 今時のWebUIは非同期更新抜きには語れない
    - テストを書く人がテスト対象のどの操作が非同期か把握し適切なwaitを指定するのは負担高い
    - だからテスト記述を「デフォルトで4秒の間リトライを繰り返すコマンド」の組み合わせで記述する
    - これで同期非同期の区別は不要になる
- 宣言的に記述
    - テストケースは生のJSで手続き的に記述するのではなく、
    - jQuery的なメソッドチェーンでコマンドとアサーションを繋ぐことで宣言的に記述する。
    - コードの見かけは同期的だが、同期的にテスト内容を構築して、その後それが非同期的に実行される。
    - これはつまり「同期的にPromiseのチェーンを作るけど、それがresolveされるのは後で非同期的」ってのと同じ。
    - なのでメソッドチェーンで表現できないことをやりたい時にはthenメソッドに関数を渡す形になる。

- CypressはURL指定でサーバにアクセスしてそれに対してテストする
    - 他のテストランナーでは特定のコンポーネントをrenderして、それに対してテストをする形があるが、Cypressではその機能はアルファ版だしjsdomを使うので僕の目的には合わない [doc](https://docs.cypress.io/guides/component-testing/introduction)
    - window.app.foobar的な形で露出してる値に対してはテストできる
        - 露出してない内部状態にアクセスする方法は、多分ないと思う
            - テスト側から見るとテスト対象はブラックボックス。
        - spyなどのツールはあるが露出してる値にしか使えないので少し制限が強い

- ソースコード編集したら自動でテストが再実行される
    - テストにこけた時にそこから普通にchrome devtoolでinspectしたりできる
    - もはや普通のブラウザを人間が操作して動作確認なんかしないでまずテストを書いた方が良いのではないか


JavaScript End to End Testing Framework [https://www.cypress.io/](https://www.cypress.io/)
> Cypress does not use [[Selenium]].
> Whereas Selenium executes remote commands through the network, Cypress runs in the same run-loop as your application.
[https://www.cypress.io/how-it-works/](https://www.cypress.io/how-it-works/)

[Introduction to Cypress | Cypress Documentation](https://docs.cypress.io/guides/core-concepts/introduction-to-cypress)
> This is the single most important guide



できた
![image](https://gyazo.com/b39c9e4c072c6cb62a32e71ab249b5d4/thumb/1000)
できた
- 最初にマウントされたあとuseEffectでフォントサイズを更新している付箋について、その更新後のフォントサイズをテストすることができた。3回visitから繰り返してるのに1秒も掛からずに3つのテストが完了しててすごい。
- [[wait(0)を削ると失敗する]]
    - wait(0)がどういう役割をしているのかわからない
    - [['cy' is not defined]]の解決のためにCypress用のeslintプラグインを入れたら「waitするのはやめろ」と言われるようになった
    - ドキュメントを見るとアサーションが失敗した時にはリトライが行われるように思えるが、なぜ期待した挙動にならないのか
        - firstでエレメントを掴んだ後でその手前に別のエレメントが現れた時にリトライしてもfirstが指すものが変わらないのかな
        - サンプルの早い段階で似たような話が書いてあった気がする
- ver. 2
    - テスト用のIDをつけるようにした
js

```javascript
/// <reference types="cypress" />

describe('adjust font size', () => {
  beforeEach(() => {
    cy.visit('/')
  })

  it('first fusen', () => {
    cy.get('.fusen[data-testid=">あ"]').should("have.css", "font-size", "66px")
  })
})
```

- another patten
    - NG:
        - `cy.get('.fusen').eq(1).should("have.css", "font-size", "53px")`
        - Timed out retrying after 4000ms: Expected to find element: 1, but never found it. Queried from element: <div#hidden-fusen.fusen>
    - OK:
        - `cy.get('.fusen').should('have.length', 12).eq(1).should("have.css", "font-size", "53px")`
- リトライが行われるのは最後のコマンドだけである
    - > Cypress commands only retry the last command before the assertion
        - [https://docs.cypress.io/guides/core-concepts/retry-ability#Only-the-last-command-is-retried](https://docs.cypress.io/guides/core-concepts/retry-ability#Only-the-last-command-is-retried)
    - これだ
    - 「リトライが行われるのは最後のコマンドだけである」を「チェーン全体がリトライされる」と勘違いしていたことが問題の原因
    - コマンドが複数連続している時に最初のがリトライされない。


[Assertions | Cypress Documentation](https://docs.cypress.io/guides/references/assertions)




-----
[Cypress入門～初心者でも簡単にE2Eテストが作れる～ | フューチャー技術ブログ](https://future-architect.github.io/articles/20210428a/)
- [[E2Eテスト]]

[Cypress - 設定編 | フューチャー技術ブログ](https://future-architect.github.io/articles/20210428b/)
- 設定でbaseUrlを指定することでテストコードにハードコードされないようにする
- mocha+chaiとjestでexpectなどがぶつかるのでtsconfigを分ける
- 頻出の操作パターンはコマンドとして定義することもできる、ただしTSで型エラーになるので型定義ファイルが必要
    - 🤔普通に関数にまとめたらいいのでは…
        - わざわざ型定義してまでcyのメソッドにするメリットがわからない

[保守・拡張をしやすいカプセル化したCypress | フューチャー技術ブログ](https://future-architect.github.io/articles/20210428c/)
- 🤔カプセル化って言葉をどういう意味で使ってるのか
    - データと手続きをまとめるという意味でもないし、アクセスを制限するという意味でもない、単に「まとめました」ということなのだろうか？

[Cypress - 書きやすいテストの秘密と独自コマンドの実装 | フューチャー技術ブログ](https://future-architect.github.io/articles/20210428d/)
- @testing-library/cypress ある
- > CypressはWebDriver系(Selenium)やChrome DevTool Protocol系（Puppeteer)のツールとAPIの粒度が異なります。
- Cypressのリトライポリシー
- 宣言的な書き方は、失敗した時のフィードバックが弱い
- ログの出力はCypress.log

[React + TypeScript + Cypress で始める E2E テスト - GiXo Ltd.](https://www.gixo.jp/blog/16086/amp/)


[[ブラウザテスト]]

