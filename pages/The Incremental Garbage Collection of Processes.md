
[PDF](https://citeseerx.ist.psu.edu/document?repid=rep1&type=pdf&doi=0236335b815ef41e86f0fe41e53a2acc1d4742f6) 1977
今ではJavaScriptのPromiseという形で有名になった概念を提案した論文。
- ユーザが式を与えると即座に「future」が返される
- これは「後で値を提供する」という約束
- プリミティブの+のようにfutureの明示的な値を必要とした場合に、それが完了しているなら即座に値を利用可能で、完了してないなら完了するまで待つ





本論文では、call-by-nameやcall-by-valueとは異なる「future」オーダーと呼ばれる引数評価順序に関連するいくつかの問題を検討する。
call-by-futureでは、関数の各形式パラメータは、対応する引数の評価専用の別プロセス（「future」と呼ばれる）に束縛される。
この機構により、関数への引数の完全な並列評価が可能となり、言語の表現力を増大させることが示されている。
この文脈で生じる問題へのアプローチとして、作成時には関連性があると考えられていた未来が、それが束縛されていた式の本体では無視されることで無関係になるという問題を取り上げる。無関係なプロセスの問題は、マルチプロセッシングの問題解決システムにも現れ、同じ問題に対して複数のプロセッサが異なる手法で処理を開始し、最初に終了した解を返すというものである。この並列手法戦略には、負けた手法を調べているプロセスを特定し、停止させ、より有用なタスクに再割り当てしなければならないという欠点がある。
我々が提案する解決策は、ガベージコレクションである。我々は、ガベージコレクションアルゴリズムが、どのプロセスが有用な作業を行っており、どれが新しいタスクのためにリサイクルできるかを発見できるように、解決策のゴール構造をグラフメモリの一部としてメモリ上で明示的に表現することを提案する（Lispのヒープのような）。
ストレージとプロセスの統一的なガベージコレクションのためのインクリメンタルアルゴリズムが説明される。

> This paper investigates some problems associated with an argument evaluation order that we call "future' order, which is different from both call-by-name and call-by-value. In call-byfuture, each formal parameter of a function is bound to a separate process (called a "future") dedicated to the evaluation of the corresponding argument. This mechanism allows the fully parallel evaluation of arguments to a function, and has been shown to augment the expressive power of a language.
>  We discuss an approach to a problem that arises in this context: futures which were thought to be relevant when they were created become irrelevant through being ignored in the body of the expression where they were bound. The problem of irrelevant processes also appears in multiprocessing problem-solving systems which start several processors working on the same problem but with different methods, and return with the solution which finishes first. This parallel method strategy has the drawback that the processes which are investigating the losing methods must be identified, stopped, and reassigned to more useful tasks.
>  The solution we propose is that of garbage collection. We propose that the goal structure of the solution plan be explicitly represented in memory as part of the graph memory (like Lisp's heap) so that a garbage collection algorithm can discover which processes are performing useful work, and which can be recycled for a new task.
>  An incremental algorithm for the unified garbage collection of storage and processes is described.
>


More precisely, a future is a 3-tuple (process, cell, queue), where process is the virtual processor initialized to evaluate this argument expression in its proper environment, cell is a writable location in memory which will save the value of the argument after it has been computed to avoid recomputing it, and queue is a list of the processes which are waiting for the value of this future. A future's process starts evaluating its expression in the given environment. If any other process needs the value of this future, and the value is not yet ready, the requesting process enters the queue of the future and goes to sleep. When the value promised by the future is ready, its process stores the value into its cell, wakes up all processes waiting in its queue, and dies.
Henceforth, any process needing this future's value can find it in the future's cell without waiting or further computation.
