---
title: "BUG:投げ縄選択で選択が行われている状態で、付箋の追加をすると、画面上に移動できないゴミ付箋が作られる"
---

from [[pRegroup-done-2019]]
- BUG:投げ縄選択で選択が行われている状態で、付箋の追加をすると、画面上に移動できないゴミ付箋が作られる
    - 投げ縄選択の描画のためにオーバーレイキャンバスがカレントプロジェクトになっていて、付箋がオーバーレイキャンバスに作られてしまうから
- アクティブなプロジェクトが間違っていることによるバグは、そもそも「アクティブなプロジェクト」というグローバルな状態があることが問題であって、アクティブなプロジェクトの切り替えオーバーヘッドは高くないのだからデフォルトのプロジェクト以外に触る関数が関数内で一時的に切り替え、戻してから終了すべき
- むしろそれをやるデコレータ的関数を使って、グローバルな状態を直接いじるのをやめるべき
    - onOverlayCanvas
- →done
