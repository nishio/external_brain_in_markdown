
from [[pRegroup-done-2019]]
[[Reconciler]]の中で作られるインスタンスはどこでアクセスするか
react-paper-bindingsはReconcilerのcreateInstanceのなかでPaper.jsのRasterのインスタンスを作って返している
- ここで返されたオブジェクトにはどこでアクセスできるのか
- [https://github.com/react-paper/react-paper-bindings/blob/50c16e349b0ceb1bf06c08de0ef7981b02985bf6/src/PaperRenderer.js#L317](https://github.com/react-paper/react-paper-bindings/blob/50c16e349b0ceb1bf06c08de0ef7981b02985bf6/src/PaperRenderer.js#L317)
- これはReactのReconcilerの仕様を調べる必要があるのだな
    - (JSXの<Raster>の返り値は当然このインスタンス自体ではなくReactが作ったオブジェクトになっていた)
- refで外部の変数に参照を渡す
    - [How to Get a React Component's Element](https://davidwalsh.name/get-react-component-element)
- [[ref]]を「DOMへの参照」みたいな解釈をしている解説があるが、DOMへの参照なのではなく、Reconcilerの中で作られるオブジェクトへの参照で、Webアプリを作る文脈ではそれがDOMであるというだけのこと
