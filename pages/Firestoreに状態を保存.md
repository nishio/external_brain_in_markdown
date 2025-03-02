---
title: "Firestoreに状態を保存"
---

from [[pKeicho-done]]
[[Firestoreに状態を保存]]
ローカルのサーバからHerokuにデプロイした際にgunicornを挟んだことでpreforkされたため記憶が分割されてしまった。サーバプロセス内に記憶を持つのではなく外に出す必要がある。
