---
title: "pKozaneba2025-09-11"
---

![image](https://gyazo.com/f4fea44776b9e5848bf2384379de4dc7/thumb/1000)
Merge の挙動変更
- 以前: Merge は常に新しい kozane を作成し、選択中のすべての kozane を削除していた。
- 変更後: scale 値が最大の kozane が残り、その他は削除される。
- エッジケース: 最大の scale が複数ある場合、テキスト結合ロジックはその最大の kozane 群にのみ適用され、最初のものが残る。
    - [https://github.com/nishio/kozaneba/pull/33](https://github.com/nishio/kozaneba/pull/33)
- 新しい挙動
    - ![image](https://gyazo.com/33e95419f0a3af5b67ecc170813d45f1/thumb/1000)
以前の挙動
- ![image](https://gyazo.com/ded5d51cbee922f67ba98071571fa28d/thumb/1000)

Group メニューに「Scale Double」コマンドを追加
- グループのコンテキストメニューに新規「Scale Double」を追加。グループ内アイテムの間隔（位置）とサイズ（スケール）を両方とも 2 倍にする。
- 既存の「Spread」はアイテム間の間隔のみを 2 倍にするため、それを補完する位置づけ。
- ![image](https://gyazo.com/adcf718feb2429a8babed153f70439e7/thumb/1000)
- [https://github.com/nishio/kozaneba/pull/34](https://github.com/nishio/kozaneba/pull/34)

Selection メニューにも Rotate／Spread／Scale Double を追加
- [https://github.com/nishio/kozaneba/pull/35](https://github.com/nishio/kozaneba/pull/35)



![image](https://gyazo.com/9022c40e054c10cac7ebff0a70d6321e/thumb/1000)
いやー、どうしたもんかな
- 線を引いた時にダイアログで聞いてくる実装をDevinが作ってくれたけど、明らかにウザい
- 「ラベル付き線」「ラベル付き矢印」の追加メニューをつけるか
- 線をクリックして「ラベルをつける」メニューがでるようにするか
