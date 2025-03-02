
Unhandled Rejection (DataError): Failed to execute 'add' on 'IDBObjectStore': Evaluating the object store's key path did not yield a value.

[[Dexie.js]]経由で[[IndexedDB]]にデータを書き込もうとしたときに出たエラー、
他のプロジェクトで同様のコードで問題なく書き込めていたので困惑

原因は、サンプルコードがデータベースに対してつけていた名前"MyAppDatabase"を使い回していたことと、開発サーバとしてlocalhost:3000を使い回していたこと
両方が同一なことで「他のプロジェクト」で作ったデータベースが見えており、そのためこのプロジェクト用のデータベースが作成されず、スキーマの違うデータベースに書き込もうとしてエラー、という現象

スキーマがたまたま同じだったらもっとややこしいバグになり得たので、データベースにはちゃんとプロジェクトが識別できる名前をつけよう

