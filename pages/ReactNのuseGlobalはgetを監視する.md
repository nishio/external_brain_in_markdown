
ReactNのuseGlobalにおいて、`useGlobal("foo")` とプロパティを明示するのではなく `useGlobal()` と省略して呼び出した場合、ReactNは返したグローバル値に対するgetのアクセスを監視して`addPropertyListener`する。

というわけで「`useGlobal()`したらすべての更新で再描画が走っちゃう？」という懸念は不要だった。

useGlobal
use-global.ts

```typescript
export default function _useGlobal<...>(...): UseGlobal<G, Property> {
  ...
  if (typeof property === "undefined") {
    ... 
    return [globalStateManager.spyState(forceUpdate), globalStateSetter];
  }
```


spyState
global-state-manager.ts

```typescript
  public spyState(propertyListener: PropertyListener): G {
    // When this._state is read, execute the listener.
    return objectGetListener(
      this._state,
      (property: keyof G) => {
        this.addPropertyListener(property, propertyListener);
      },
    );
  }
```


objectGetListener
object-get-listener.ts

```typescript
// Return an object that executes a read listener.

export default function objectGetListener<Shape>(
  obj: Shape,
  listener: Function,
): Shape {
  return (Object.keys(obj) as (keyof Shape)[]).reduce(
    (accumulator: Partial<Shape>, key: keyof Shape): Partial<Shape> => {
      Object.defineProperty(accumulator, key, {
        configurable: false,
        enumerable: true,
        get: (): Shape[keyof Shape] => {
          listener(key);
          return obj[key];
        }
      });
      return accumulator;
    },
    Object.create(null)
  );
};
```


[[ReactN]]の[[reactn]]
