---
title: "Over 200 classes were generated"
---

:

```
Over 200 classes were generated for component styled.div with the id of "sc-jrsJWt".
Consider using the attrs method, together with a style object for frequently changed styles.
Example:
  const Component = styled.div.attrs(props => ({
    style: {
      background: props.background,
    },
  }))`width: 100%;`
```


[[styled-components]]がよくわかってなくてこんなことを書いていたのだが、これをやると異なるpropsごとに異なるクラスが作られてしまうので適切でない
ts

```typescript
export const KozaneDiv = styled.div`
  ...
  top: ${(props) => props.style?.top ?? "0px"};
  left: ${(props) => props.style?.left ?? "0px"};
```


こんなのをわざわざ書かなくてもstyleは最終的なDOM Elementのstyleに当たるので、単に削除でいい。