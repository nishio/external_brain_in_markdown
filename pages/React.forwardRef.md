---
title: "React.forwardRef"
---

どういう時に要求されるのかよくわからない
ts

```typescript
type PropsType = { id: ItemId };
export const BigMenuItem = React.forwardRef<HTMLLIElement, PropsType>(
  ({ id }, ref) => {
    const onBig = () => {
      updateGlobal((g) => {
        const item = get_item(g, id);
        item.scale++;
      });
      close_menu();
    };

    return (
      <MenuItem onClick={onBig} ref={ref} data-testid="big">
        big
      </MenuItem>
    );
  }
);
```


---
React.forwardRefは、型としては関数コンポーネントを引数に取れないようだ。実装としては取れる。

`function React.forwardRef<unknown, {}>(render: React.ForwardRefRenderFunction<unknown, {}>): React.ForwardRefExoticComponent<React.RefAttributes<unknown>>`

引数にReact.FCを指定するとエラーになる。
> Argument of type 'FC<Props>' is not assignable to parameter of type 'ForwardRefRenderFunction<unknown, Props>'.
ts

```typescript
const _MenuItem: React.FC<Props> = (props) => {
  const { title, onClick, ref, ...other } = props;
  const f = () => {
    handleClose();
    onClick();
  };
  return (
    <MenuItem onClick={f} {...other} ref={ref}>
      {title}
    </MenuItem>
  );
};

export const AutoCloseMenuItem = React.forwardRef(_MenuItem);
```


同じ実装でも型をFCだと宣言しなければOK
ts

```typescript
const _MenuItem = (props: Props) => {
	... // (same)
};

export const AutoCloseMenuItem = React.forwardRef(_MenuItem);
```


2021-09-01追記
- これ、型チェックがないせいで第二引数のrefを暗黙に捨ててるだけじゃん
