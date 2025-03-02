---
title: "TypeScriptのType"
---

structual subtyping

interface
- 宣言したプロパティがないとエラー
- 宣言してないプロパティがあってもエラー
- Optional: なくてもいい

union
- 二つの方のどちらかであればよい

intersection
- Intersection types have the following subtype relationships:
    - An intersection type I is a subtype of a type T if any type in I is a subtype of T.
    - A type T is a subtype of an intersection type I if T is a subtype of each type in I.
- Similarly, intersection types have the following assignability relationships:
    - An intersection type I is assignable to a type T if any type in I is assignable to T.
    - A type T is assignable to an intersection type I if T is assignable to each type in I.



- [https://stackoverflow.com/questions/37233735/typescript-interfaces-vs-types](https://stackoverflow.com/questions/37233735/typescript-interfaces-vs-types)
- typeは新しい型のインスタンスを作るのではなく、単に別の型にエイリアスを作るだけ
    - オブジェクトリテラルの型の別名を作った場合に、その見た目がinterfaceに似ているために混乱している人がいる