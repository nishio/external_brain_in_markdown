---
title: "NullPointerException"
---

たとえばPerson型の変数がある場合、人間は暗黙に「値としてPersonクラスのインスタンスが入っている」と思い込みがち
ところがJavaの場合、実際には「Personクラスのインスタンス、もしくはnullが入っている」だった
この勘違いによって実行時にNullPointerExceptionが出る

かの問題を解決するために「[[Nullable]]な型とそうでない型を区別しよう」となった

