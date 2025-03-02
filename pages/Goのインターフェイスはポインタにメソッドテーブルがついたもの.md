
[[Goのインターフェイス]]は[[ポインタ]]に[[メソッドテーブル]]がついたもの
[[インターフェイス]]という言葉で[[Javaのインターフェイス]]をイメージすると混乱する。

go

```
// emptyInterface is the header for an interface{} value.
type emptyInterface struct {
	typ  *rtype
	word unsafe.Pointer
}

// nonEmptyInterface is the header for an interface value with methods.
type nonEmptyInterface struct {
	// see ../runtime/iface.go:/Itab
	itab *struct {
		ityp *rtype // static interface type
		typ  *rtype // dynamic concrete type
		hash uint32 // copy of typ.hash
		_    [4]byte
		fun  [100000]unsafe.Pointer // method table
	}
	word unsafe.Pointer
}
```

[https://github.com/golang/go/blob/7e987b7/src/reflect/value.go#L180-L197](https://github.com/golang/go/blob/7e987b7/src/reflect/value.go#L180-L197)

C言語に縛って検索してて中々見つからないなと思ったのだが、*.goの中にあったのか。

