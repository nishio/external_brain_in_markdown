
Type instantiation is excessively deep and possibly infiniteの最小限の例
リストの先頭が順次削られていくので有限回で確実に終了するがTypeScriptがそれを理解できない
- F単体ではTypeScriptもexcessively deepとは判断しない
- Gで同じことをやってからFに渡している
    - ここでexcessively deepと判断される
    - 実際にはFに渡す前に`[0, []]`になるのでさほど深くならない

ts

```typescript
type LIST = [0, []] | [0, LIST]
type F<N extends LIST> = (
  {
    0: F<N[1] extends LIST ? N[1] : never>,
    1: [0, []]
  }[N[1] extends LIST ? 0 : 1]
)

type G<N extends LIST> = (
  F<
    {
      0: G<N[1] extends LIST ? N[1] : never>,
      1: [0, []]
    }[N[1] extends LIST ? 0 : 1]
  >
)
```



:

```
Type instantiation is excessively deep and possibly infinite.

Type '{ 0: { 0: { 0: { 0: { 0: { 0: { 0: { 0: { 0: { 0: { 0: { 0: ...[((((((((((({ 0: ...[{ 0: ...[{ 0: ...[{ 0: ...[{ 0: ...[{ 0: ...[{ 0: ...[{ 0: ...[{ 0: ...[{ 0: ...[...[(((((((((((N[1] extends LIST ? N[1] : never)[1] extends LIST ? (N[1] extends LIST ? N[1] : never)[1] : never)[1] extends LIST ? ((N[1] extends LIST ...' does not satisfy the constraint 'LIST'.
 Type '{ 0: { 0: { 0: { 0: { 0: { 0: { 0: { 0: { 0: { 0: { 0: { 0: ...[((((((((((({ 0: ...[{ 0: ...[{ 0: ...[{ 0: ...[{ 0: ...[{ 0: ...[{ 0: ...[{ 0: ...[{ 0: ...[{ 0: ...[...[(((((((((((N[1] extends LIST ? N[1] : never)[1] extends LIST ? (N[1] extends LIST ? N[1] : never)[1] : never)[1] extends LIST ? ((N[1] extends LIST ...' is not assignable to type '[0, LIST]'.
```

