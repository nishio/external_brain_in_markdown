
失敗しうる関数が失敗の情報を返すための型
[[Rust]]が例外機構を持たずにこれに寄せてるが、Rustが初めてではない
- 何が始めたんだろ、MLあたりかな

[Error Handling · OCaml Tutorials](https://ocaml.org/docs/error-handling)
> The Stdlib module contains the following type:
ocaml

```
type ('a, 'b) result =
  | Ok of 'a
  | Error of 'b
```

