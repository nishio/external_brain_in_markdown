---
title: "Netlifyでデプロイ"
---

Netlifyでデプロイしようとしたらpackage.jsonとかがおかしくて
すんなりnpm run buildできる状態ではなかった

念の為メモ
:

```
Could not find a declaration file for module 'paper'. '/Users/nishio/foobar/regroup/regroup/node_modules/paper/dist/paper-full.js' implicitly has an 'any' type.
  Try `npm install @types/paper` if it exists or add a new declaration (.d.ts) file containing `declare module 'paper';`ts(7016)
```


:

```
$ npm install --save @types/paper
npm WARN deprecated @types/paper@0.12.3: This is a stub types definition. paper provides its own type definitions, so you do not need this installed.
+ @types/paper@0.12.3
```


:

```
Cannot find namespace 'paper'.  TS2503

  >  9 | let positionOfNewPiece: paper.Point | null = null;
       |                         ^
```


diff

```
-    "paper": "0.12.0",
+    "paper": "^0.12.4", 
```


:

```
'ToolEvent' refers to a value, but is being used as a type here.  TS2749
    23 | type Handler = {
  > 24 |   onDrag: (event: ToolEvent, dragStartPoint: paper.Point) => void,
       |                   ^
```


diff

```
-    "paper": "^0.12.4", 
+    "paper": "0.12.0",
```


diff

```
-   "@types/paper": "^0.12.3",
+    "@types/paper": "0.11.8",

```


:

```
Property 'Tool' does not exist on type 'PaperScope'. Did you mean 'tool'?  TS2551

    28 | 
    29 | let createDefaultTool = (updateStateItem: any): paper.Tool => {
  > 30 |   let tool = new window.app.paper.Tool();
       |                                   ^
```


diff

```
- import { ToolEvent } from "paper";
+ import { ToolEvent, Tool } from "paper";

- let tool = new window.app.paper.Tool();
+ let tool = new Tool();
```


[[pRegroup-done-2020]]

from [[paper.jsの型定義]]