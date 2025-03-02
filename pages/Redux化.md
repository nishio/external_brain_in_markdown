---
title: "Redux化"
---

こんな感じですかね。 [[Redux]]+[[TypeScript]]

ts

```typescript
import { createStore } from 'redux';
...

export const initialState = {
	...
};

export type StateType = typeof initialState;

enum ActionType {
  SET_ITEMS = "SET_ITEMS",
}

export const setItems = (items: StateItem[]) => {
  return { type: ActionType.SET_ITEMS, payload: items }
}

interface Action {
  type: ActionType;
  payload: any;
}

function rootReducer(state = initialState, action: Action) {
  switch (action.type) {
    case ActionType.SET_ITEMS:
      return { ...state, items: action.payload };
    default:
      return state;
  }
}

export const store = createStore(rootReducer);
```


[[pRegroup-done-2019]]
