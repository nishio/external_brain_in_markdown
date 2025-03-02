

[Mixins - TypeScript Deep Dive 日本語版](https://typescript-jp.gitbook.io/deep-dive/type-system/mixins)
クラスを引数に取ってクラスを返す関数として実現されている
サンプルに書かれてるやり方では、他のMixinが提供するメンバにアクセスすることが(型を無視しない限り)できないので微妙

ts

```typescript
type Constructor<T = {}> = new (...args: any[]) => T;
function Mixin1<TBase extends Constructor>(Base: TBase) {
  return class extends Base {
    a = 1;
  };
}
function Mixin2<TBase extends Constructor>(Base: TBase) {
  return class extends Base {
    foo() {
      // return this.a; // NG: Property 'a' does not exist on type '(Anonymous class)'
    }
  };
}

class BaseClass {
  b = "";
}

const NewClass = Mixin2(Mixin1(BaseClass));
```


混ぜ込み対象クラスがaを持ってることを型で保証することはできる
ただし条件が充足されてるかのテストが混ぜ込みごとに起こるので、充足される順で混ぜ込む必要があって微妙
ts

```typescript
type HasA<T = { a: number }> = new (...args: any[]) => T;

function Mixin2<TBase extends HasA>(Base: TBase) {
  return class extends Base {
    foo() {
      return this.a; // OK
    }
  };
}

const NewClass = Mixin2(Mixin1(BaseClass));  // OK
// const NewClass2 = Mixin1(Mixin2(BaseClass));  // NG: Property 'a' is missing 
```


レシーバを明示的に渡すスタイルならできる
ts

```typescript
const supplyA = { a: 1 };
const demandA = { foo: (self: { a: number }) => self.a };

const obj = { ...demandA, ...supplyA } as typeof demandA & typeof supplyA;
obj.foo(obj);
```


