
SVGもJSXで埋め込めるのでReactのコンポーネントにすることができる。
propsで色が変わるようにするのも特に他のDOMのコンポーネントと変わらない。

tsx

```
export const UndoSVGButton = (props: any) => {
  let color = props.enabled ? "#000" : "#888";
  return (<svg enable-background="new 0 0 24 24" id="Layer_1" version="1.0" viewBox="0 0 24 24">
    <polygon points="9,12 2,7 9,2 " fill={color} />
    <path d="M2,20h11.5c3.6,0,6.5-2.9,6.5-6.5S17.1,7,13.5,7H6"
      fill="none" stroke={color}
      stroke-miterlimit="10" stroke-width="4" />
  </svg>);
}
```


使い方
:

```
<div id="toolbar">
  <UndoSVGButton enabled={canUndo} onClick={undo} />
  <RedoSVGButton enabled={canRedo} onClick={redo} />
  ...
```


以前はテキストとCSSでやっていたのだが、コードも見た目も美しくなかった
:

```
<span onClick={undo} className={canUndo ? "canDo" : "canNotDo"}>[Undo]</span>
```

UndoとRedoはまだテキストのままなんだけどもそのうちアイコンに置き換えようと思う
![image](https://gyazo.com/23cad50452da5b3c77942de52fc9b073/thumb/1000)
関連: [[テキストの垂直中揃え]]
