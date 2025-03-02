
> Warning: Function components cannot be given refs. Attempts to access this ref will fail. Did you mean to use React.forwardRef()?

[[Material-UI]]のMenuが子要素にrefをインジェクトしようとして、それが関数コンポーネントの時に警告される。
ts

```typescript
      <Menu ... >
        <MyMenuItem onClick={exportForRegroup}>Export for Regroup</MyMenuItem> 
```


ts

```typescript
  const MyMenuItem = (props: any) => {
    const { children, onClick, ...other } = props;
    const f = () => {
      onClick();
      setAnchorEl(null);
    };
    return (
      <MenuItem onClick={f} {...other}>
        {children}
      </MenuItem>
    );
  };
```


修正
警告メッセージのとおりReact.forwardRefでrefを転送する
ts

```typescript
  const MyMenuItem = React.forwardRef((props: any, ref) => {  // here
    ...
    return (
      <MenuItem onClick={f} {...other} ref={ref}>  // here
        {children}
      </MenuItem>
    );
  });
```


