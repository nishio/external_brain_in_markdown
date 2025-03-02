---
title: "wait(0)を削ると失敗する"
---

js

```javascript
describe('adjust font size', () => {
  beforeEach(() => {
    cy.visit('/')
    // cy.wait(0) // THIS
  })

  it('first fusen', () => {
    cy.get('.fusen').first().should("have.css", "font-size", "66px")
  })

```


without wait(0)
![image](https://gyazo.com/2e442aa6fdfa6f0d2e91538058d09b26/thumb/1000)

with wait(0)
![image](https://gyazo.com/fcb7795a50d64eb212a0ac9bf185326e/thumb/1000)

