
型がついてればいいってもんじゃない
ts

```typescript
const makeV = (f: boolean) => {
  if (f) {
    return { x: 1, y: 1 };
  } else {
    return {};
  }
};

const v = makeV(true);
const x = v.x; // x: number | undefined
```


anyで受けてたせいで名前のついてない中途半端な形のオブジェクトが通されてる(変数名xなのも雑
ts

```typescript
type FIXME = {
  nameplate: number | null;
  isOpen: boolean;
};

export const createNewGroupStateItem = (
  position: paper.Point,
  items: number[] | StateItem[],
  x: FIXME,
): GroupStateItem => {
  return createGroupStateItem(position, items, x, createUniqueID());
};

export const createGroupStateItem = (
  position: paper.Point,
  items: number[] | StateItem[],
  x: FIXME,
  id: ItemID,
): GroupStateItem => { ... 
```



ts

```typescript
import { ToolEvent } from "paper";
export const isTwoFingerGesture = (event: ToolEvent) => {
  const e: any = (event as any).event;
```



ts

```typescript
export const convertStateItemToFirestore = (x: StateItem) => {
  const ret: any;
  ret.type = x.type;
  ret.id = x.id;
  ret.position = [x.position.x, x.position.y]
  if (isPieceStateItem(x)) {
    ret.text = x.text;
	...	
  } else if (isPathStateItem(x)) {
    ret.opacity = x.opacity ?? 1.0;
	...
  }
  return ret;
```


ts

```typescript
export const createBlankFirestore = (): FIRESTORE_DOC => {
  const ret: any = {
    version: 2,
  };
  ret.itemStore = {};
  ret.drawOrder = [];
  return ret;
};
```

ts

```typescript
export const createBlankFirestore = (): FIRESTORE_DOC => {
  const version = 2;
  const itemStore = {};
  const drawOrder: ItemID[] = [];
  return { version, itemStore, drawOrder };
};
```


ts

```typescript
export const onOverlayCanvas = (f: (...args: any[]) => unknown) => {
  return (...args: unknown[]) => {
    paper.projects[1].activate();
    const ret = f(...args);
    paper.projects[0].activate();
    return ret;
  };
};
```

ts

```typescript
import { ToolEvent } from "paper";

export const onOverlayCanvas = <T extends [ToolEvent] | []>(
  f: (...args: T) => unknown,
) => {
  return (...args: T) => {
    paper.projects[1].activate();
    const ret = f(...args);
    paper.projects[0].activate();
    return ret;
  };
};
```


