
`Function DocumentReference.set() called with invalid data. Data must be an object, but it was: a custom Object object`

not work
- `firebase.firestore().collection("foo").doc("bar").set({})`
- hacks also don't work
    - `Object.assign({}, obj)`
    - `JSON.parse(JSON.stringify(obj))`

correct insight
> This is likely a cross-window issue: GWT code runs in an iframe; if Firebase is looking for a "bare object", it likely compares the object's constructor, which won't be the expected one if the object crosses the iframe boundary.
- [https://stackoverflow.com/questions/46620162/firestore-web-code-sample-gives-invalid-argument-type](https://stackoverflow.com/questions/46620162/firestore-web-code-sample-gives-invalid-argument-type)

Cypress also uses iframes. So we can't store objects created in testcases.
