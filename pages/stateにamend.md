
from [[付箋の追加をPaper.js上で実装する]]
stateにamend
画面を開くことによるstateの変更と、付箋の追加によるstateの変更が別個にHistoryに入ってしまうので、Undoするとそれぞれ別にUndoされる。ユーザの1操作で複数のstate変更が起こるときはgit commit --amendみたいになった方が良い気がする

Undoの単位を変える件、「Undoの単位を変える」って考えるより
プログラム上でAとBの変更を発生させて、「Aだけ終わってる状態」にUndoで戻る必要がないなら
Aの直後でUndoのためのHistoryから1個popすれば良いだけだと思った

[[pRegroup2020]]
