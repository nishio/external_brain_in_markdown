
`<IconButton>`の中に`<Menu>`が入っていたため、MenuItemをクリックしてメニューを閉じる処理をした後で、そのクリックイベントがPropagateして、もう一度メニューを開く処理をしている

stopPropagationでも良いが、そもそも`<IconButton>`の中に`<Menu>`を入れることが想定外なのだと判断して`<>...</>`で並べて置いた。

[[Material-UI]]
