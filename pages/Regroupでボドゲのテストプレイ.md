---
title: "Regroupでボドゲのテストプレイ"
---

![image](https://gyazo.com/cbb8a5075f0e18f2b399d7b0e57d0623/thumb/1000)
readonly: [https://regroup.netlify.com/#/key=rUbCZKBwCyxrml2dCIPJ&cx=-493&cy=-31&top=-816&left=-2103](https://regroup.netlify.com/#/key=rUbCZKBwCyxrml2dCIPJ&cx=-493&cy=-31&top=-816&left=-2103)

最近[BGEngine | ボードゲーム作成支援](https://bgengine.net/)を使ってリモートでボードゲームのテストプレイをしていて、リモートでも問題なくボドゲができるなーと思った
Regroupでも似たことができそうな気がしたので作ってみた
- [[画像付箋の原寸表示]]を追加
    - Scrapboxに貼ったカード画像一覧をインポート
- [[コピー＆ペースト]]
    - 赤と青のチップを増やすのに使った
- [[矢印がグループ化されてると、ひとかたまりのものとして移動できて便利]]
    - ライフカウンターの矢印がひとかたまりのコンポーネントになってる

専用に特化したBGEngineと比較すると
- カードを裏返す機能
- 山札のシャッフル機能
などはない
隠れ情報がないゲームしかRegroupではできない

Regroupの共同編集は、サーバに後から来たもので上書きされるので同時に編集するとおかしくなるが、ペンで書いたものが上書きで消えるのに比べて、カードの移動は問題起きにくいし、そもそもこのゲームがターン制なので同時編集が起きにくい
