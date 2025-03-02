---
title: "Result型"
---

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



GPT4に説明させたら長文ができてしまったが有益なので記録しておく
<img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>Result 型は、プログラミング言語 Rust において、操作が成功した結果を返すか、何らかの理由で失敗した際にエラーを返すことができる列挙型（enum）です。これはエラーハンドリングをより安全かつ効果的に行うために使われます。

Result 型は次のように定義されています：
rust

```
enum Result<T, E> {
    Ok(T),
    Err(E),
}
```

ここで、T は操作が成功した場合の戻り値の型を表し、E はエラーの型を表します。

使用例
例えば、ファイルを開く操作が失敗する可能性がある場合、その関数は Result 型を返すことが一般的です。ファイルが正常に開かれた場合は Ok バリアントを使用してファイルハンドルを返し、エラーが発生した場合は Err バリアントでエラー情報を返します。

rust

```
use std::fs::File;

fn open_file(path: &str) -> Result<File, std::io::Error> {
    let file = File::open(path)?;
    Ok(file)
}
```

この関数では、? 演算子を使用しています。この演算子は Result が Err の場合に早期リターンを行い、エラーをそのまま返します。もし Result が Ok の場合は、Ok 内の値を取り出します。

エラーハンドリング
Result 型を使う主な利点は、エラーを明示的に扱う必要があることです。これにより、エラーが無視されることなく適切に処理されることが保証されます。

rust

```
fn process_file(path: &str) {
    match open_file(path) {
        Ok(file) => {
            // ファイルが正常に開かれた場合の処理
            println!("File opened successfully!");
        },
        Err(e) => {
            // エラーが発生した場合の処理
            println!("Failed to open file: {}", e);
        },
    }
}
```

このように、Result 型を活用することで、プログラムの堅牢性を向上させ、エラーによる予期せぬ動作を防ぐことができます。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>Haskellにも似たものがあるよね

<img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>はい、HaskellにもResult型に似た概念があり、それはEither型です。Either型は、二つの値のうちの一つを保持するための汎用的なデータ型で、一般にエラーハンドリングやその他の状況で利用されます。この型は以下のように定義されています：

hs

```
data Either a b = Left a | Right b
```


ここで、Leftは通常、エラーまたは非正常な状況を表すために使われ、Rightは成功または正常な結果を表すために使われます。Either型を使うことで、関数が複数の異なる失敗モードを持つ場合に、それらを適切に表現することができます。

Haskellでの使用例
ファイルを開く操作を例に取ると、以下のようにEither型を使ってエラーを扱うことができます：

haskel

```
import System.IO
import System.IO.Error

tryOpenFile :: FilePath -> IO (Either IOError Handle)
tryOpenFile path = tryIOError (openFile path ReadMode)
```

この関数は、IOErrorをLeftでラップして返すか、成功した場合はファイルハンドルをRightで返します。

エラーハンドリング
HaskellでEither型を使ったエラーハンドリングは、パターンマッチングを通じて行います：

haskell

```
processFile :: FilePath -> IO ()
processFile path = do
    result <- tryOpenFile path
    case result of
        Left err -> putStrLn $ "Failed to open file: " ++ show err
        Right handle -> do
            putStrLn "File opened successfully!"
            hClose handle
```


この例では、tryOpenFileから返されたEither型の値をcase式で分岐しています。エラー(Left)の場合はエラーメッセージを出力し、成功(Right)の場合は成功メッセージを出力してファイルを閉じます。

このようにEither型は、Haskellでエラーハンドリングやその他の二つの結果を区別するための強力なツールです。

[[コーディングを支える技術加筆案]]
