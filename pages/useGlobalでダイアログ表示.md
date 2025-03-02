
ダイアログは「開いてる/閉じてる」という状態を持ったコンポーネントである。
通常、メニューなどの「ダイアログとは親子関係にないコンポーネント」から状態が更新される。
これをどうやるのがいいか。

案1:
- 共通の親コンポートが状態を保つ
- 子コンポーネントにはpropsで渡す
- オーソドックスなやり方だが、個人的に嫌い
    - setterをpropsで子コンポーネントに渡していくスタイルが納得できない

案2:
- ダイアログが状態をもつ
FooDialog.tsx

```
const FooDialog = () => {
  const [open, setOpen] = useState(false);
  ...
}
```

- このままではsetterがローカルスコープに閉じ込められてるので、露出する
FooDialog.tsx

```
export let openFooDialog: () => void;
const FooDialog = () => {
  const [open, setOpen] = useState(false);
  openFooDialog = () => {
    setOpen(true);
  }
  ...   
}
```

- 最近までこうやってた

案3:
- ダイアログがuseGlobalする
FooDialog.tsx

```
export const FooDialog = () => {
  const [dialog, setDialog] = useGlobal("dialog");
  const open = dialog === "Foo";
  ...
}
```

- booleanのopenを直接globalにするのではなく「開いているダイアログ」を意味する変数を導入されたした
    - ダイアログはアプリ全体で一度に一つしか開かないという想定を反映した実装
- 型で値を限定してTypoなどを防ぐ
ts

```typescript
const INITIAL_GLOBAL_STATE = {
  ...
  dialog: null as "Foo" | null,
};
```

- 開く側はsetGlobalする
ts

```typescript
export const openFooDialog = () => {
  setGlobal({ dialog: "Foo" });
};
```

- 2021-03-22にこのやり方を思いついた
- 最初は`openFooDialog`に相当するコードはメニューの側に置かれていたが、その後この名前に変えてFooDialog.tsxの中に移動した
    - どこで定義されてるダイアログを表示するのか明確になる

何が最良なのかまだピンときていないが、方針変更があったこのタイミングで記録しておくことが有益だと思って記録した
