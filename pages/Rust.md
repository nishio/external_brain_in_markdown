
2015 Rust 1.0 リリース
Rust自体は2010年リリース
同時期にC++に起こったことを見るのが良い
- 2011年のC++11
    - std::unique_ptr
        - 確保したメモリ領域を指すポインタがユニークであることが保証できるなら、スコープを抜ける時に解放して良い

C++は過去に書かれたソースコードとの互換性を保つことを重視している
- なので「unique_ptrで統一した方がいいのになぁ」と思っても、そうやるわけにはいかない
- そこでRustが生まれた
- [[不自由な手法が好まれるようになる]]の一種


[[コーディングを支える技術加筆案]]

- GC以前、参照カウント、マーク&スイープ、あたりから書く？
    - 参照カウントとshared_ptr
- [[ライフタイム]]の概念？
- RAII・参照・借用チェッカー？
    - 話をする上でRAIIなしでは難しい気がするな
    - [https://ja.wikipedia.org/wiki/RAII](https://ja.wikipedia.org/wiki/RAII)
- C++11 ムーブセマンティクス
    - 右辺値参照の話になると大部分の読者には行き過ぎかな

- C++のメモリ管理と捉えると他の言語の人が興味を失う
    - 「開けたら閉めろ」的な制約に関する
    - 「電気をつけたら消せ」
        - 「でもまだ使ってる人がいるなら消してはいけない」


[https://doc.rust-jp.rs/book-ja/ch04-00-understanding-ownership.html](https://doc.rust-jp.rs/book-ja/ch04-00-understanding-ownership.html)
> 所有権を理解する
> 所有権はRustの最もユニークな機能であり、これのおかげでガベージコレクタなしで安全性担保を行うことができるのです。 故に、Rustにおいて、所有権がどう動作するのかを理解するのは重要です。この章では、所有権以外にも、関連する機能を いくつか話していきます: 借用、スライス、そして、コンパイラがデータをメモリにどう配置するかです。

(メモ: 余計なスコープを後で消す)
rust

```
fn main() {
    {
        let x = 1;
        let y = x;
        println!("x: {}", x);
        println!("y: {}", y);
    }
}
```

output

```
x: 1
y: 1
```

rust

```
fn main() {
    {
        let x = String::from("hello");
        let y = x;
        println!("x: {}", x);  // NG
        println!("y: {}", y);
    }
}
```

error

```
error[E0382]: borrow of moved value: `x`
 --> src/main.rs:5:27
  |
3 |         let x = String::from("hello");
  |             - move occurs because `x` has type `String`, which does not implement the `Copy` trait
4 |         let y = x;
  |                 - value moved here
5 |         println!("x: {}", x);
  |                           ^ value borrowed here after move
  |
  = note: this error originates in the macro `$crate::format_args_nl` which comes from the expansion of the macro `println` (in Nightly builds, run with -Z macro-backtrace for more info)
help: consider cloning the value if the performance cost is acceptable
  |
4 |         let y = x.clone();
  |                  ++++++++
```


C++だと
cpp

```cpp
#include <iostream>
#include <string> 

int main () {
    std::string x("abc");
    std::string y;
    y = x;  // (*) copy
    std::cout << x << std::endl;  // OK
    std::cout << y << std::endl;
}
```


cpp

```cpp
#include <iostream>
#include <string> 
#include <memory> 

int main () {
    std::unique_ptr<std::string> x = std::make_unique<std::string>(std::string("abc"));
    std::unique_ptr<std::string> y;
    std::cout << *x << std::endl;
}
```

`no member named 'make_unique' in namespace 'std'`
`make_unique is an upcoming C++14 feature `
- こうか
    - `$ clang++ -std=c++14 t.cpp && ./a.out`

cpp

```cpp
#include <iostream>
#include <string> 
#include <memory> 

int main () {
    std::unique_ptr<std::string> x = std::make_unique<std::string>(std::string("abc"));
    std::unique_ptr<std::string> y;
    y = std::move(x);
    std::cout << *y << std::endl;
    std::cout << *x << std::endl;  // here
}
```

output

```
abc
Segmentation fault
```




> 他の言語を触っている間に"shallow copy"と"deep copy"という用語を耳にしたことがあるなら、 データのコピーなしにポインタと長さ、許容量をコピーするという概念は、shallow copyのように思えるかもしれません。 ですが、コンパイラは最初の変数をも無効化するので、shallow copyと呼ばれる代わりに、 ムーブとして知られているわけです。
> Rustでは、 自動的にデータの"deep copy"が行われることは絶対にないわけです。

値がスタックに置かれてるかヒープに置かれてるかを意識する必要がある
- わかってる人にとってはさほど難しいことではない
- 今まで意識していなかった人にとっては、新しく意識することが増えるわけだ

rust

```
fn main() {
    {
        let x = String::from("hello");
        foo(x);
        println!("x: {}", x);  // NG
    }
}
fn foo(x: String){
    println!("x: {}", x);
}
```

error

```
error[E0382]: borrow of moved value: `x`
 --> src/main.rs:5:27
  |
3 |         let x = String::from("hello");
  |             - move occurs because `x` has type `String`, which does not implement the `Copy` trait
4 |         foo(x);
  |             - value moved here
5 |         println!("x: {}", x);  // NG
  |                           ^ value borrowed here after move
  |
note: consider changing this parameter type in function `foo` to borrow instead if owning the value isn't necessary
 --> src/main.rs:8:11
  |
8 | fn foo(x: String){
  |    ---    ^^^^^^ this parameter takes ownership of the value
  |    |
  |    in this function
  = note: this error originates in the macro `$crate::format_args_nl` which comes from the expansion of the macro `println` (in Nightly builds, run with -Z macro-backtrace for more info)
help: consider cloning the value if the performance cost is acceptable
  |
4 |         foo(x.clone());
  |              ++++++++
```


> 所有権を取り、またその所有権を戻す、ということを全ての関数でしていたら、ちょっとめんどくさいですね。 関数に値は使わせるものの所有権を取らないようにさせるにはどうするべきでしょうか。

rust

```
fn main() {
    {
        let x = String::from("hello");
        foo(&x);
        println!("x: {}", x);  // OK
    }
}
fn foo(x: &String){
    println!("x: {}", x);
}
```


> s1の値を参照する参照を生成することができますが、これを所有することはありません。 所有してないということは、指している値は、参照がスコープを抜けてもドロップされないということです。

`cannot borrow `s` as mutable more than once at a time`
> これは、新たなRustaceanにとっては、 壁です。なぜなら、多くの言語では、いつでも好きな時に可変化できるからです。...この制約がある利点は、コンパイラがコンパイル時にデータ競合を防ぐことができる点です。 データ競合とは、競合条件と類似していて、これら3つの振る舞いが起きる時に発生します:
>  2つ以上のポインタが同じデータに同時にアクセスする。
>  少なくとも一つのポインタがデータに書き込みを行っている。
>  データへのアクセスを同期する機構が使用されていない。
>  データ競合は未定義の振る舞いを引き起こし、実行時に追いかけようとした時に特定し解決するのが難しい問題です。 しかし、Rustは、データ競合が起こるコードをコンパイルさえしないので、この問題が発生しないようにしてくれるわけです。

`cannot borrow `s` as mutable because it is also borrowed as immutable`

rust

```
fn main() {
    {
        foo();
    }
}
fn foo() -> &String{
    let x = String::from("hello");
    &x
}
```

error

```
error[E0106]: missing lifetime specifier
 --> src/main.rs:6:13
  |
6 | fn foo() -> &String{
  |             ^ expected named lifetime parameter
  |
  = help: this function's return type contains a borrowed value, but there is no value for it to be borrowed from
help: consider using the `'static` lifetime
  |
6 | fn foo() -> &'static String{
  |              +++++++
```

