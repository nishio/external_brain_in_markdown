---
title: "undoの実装"
---

[[pRegroup-done-2019]]
付箋の追加や移動をUndo可能にするReact的状態の設計
- useHistoryをTSに移植した
- 若干モヤモヤするけど早すぎる最適化は諸悪の根源なので「全状態履歴を保持する実装」でまずは作る。
- 生の状態ではなく実験的な状態でuseHistoryの挙動をまず試す
- 次に付箋をReact的な状態に変換する
- (パスもやる？？パスがかける以上、ユーザはパスをUndoしようとするだろう。状態に異種のものが混じっている状態はどうせ将来的に発生するのでシンプルな今の段階で試しておくべき→やる)


[Using React Hooks with canvas – ITNEXT](https://itnext.io/using-react-hooks-with-canvas-f188d6e416c0)
- 解説: [[React+Canvas]]
- これがReact的な状態管理で描画の永続化までやっててよい
- この方法はとてもわかりやすい反面、性能を度外視して「ユーザの操作履歴を毎回全部描く」をやっている。
- なんだけども、Paper.jsが現状、画面外のカリングとかしないで全部愚直に書いているっぽいし、ユーザとのインタラクションをするPaperはこのあと別レイヤーとして上に重ねるわけなので、まずは愚直に実装したらいいのかもな〜と思った。
- Regroupのユースケースでは「追加」だけではなく「移動」がある。
    - Undo可能にするためには「移動」を「どこからどこへの移動」という反転可能な形で保持して、
    - 実際のレンダリング前に履歴を実行して現在の位置を特定し、
    - その現在の位置から画面内に含まれてるかどうかをチェックして、
    - 含まれてるものだけ描くって処理になると思われ。
- 直近のスナップショットを保存して置いても良いと思う

undoの実装
- 特に手書きが入ると必須
- [https://usehooks.com/](https://usehooks.com/)
- これのuseHistoryパターンが良さそう
- [[useCallback]]、[[useReducer]]
- これも全ての状態を持っておいて、全体を更新するタイプ。
    - それでいいのかなぁ、修正差分にしなくていいのかなぁ、と言う気もするが、性能問題がでないならシンプルな実装の方が良いのでまずはその方針でやるべきかなぁ
    - 早すぎる最適化は諸悪の根源。

[[useHistory]]の実装がSETで状態を代入することしか考えてなくて、(state)=>(newState)がわたされる可能性を考えていない。
ts

```typescript
let newPresent;
if(typeof action.newPresent == "function"){
  newPresent = action.newPresent(present);
}else{
  newPresent = action.newPresent
}
```

こうやった

ズームがUndoできるようになった！

付箋のリストとして状態を保つのではなく「描画されるアイテムのリスト」にオブジェクトを入れてobj.typeでどういう描画をするか切り分ける設計にした。
これによって将来的に手書きパスも一貫して扱えるようになる。
付箋と手書きパスの他に将来的に現れる予定なものは
・グループ
・コネクタ

状態更新を呼んで正しく描画されてるのにUndoが機能しない
あ、元の状態を破壊的に変更してしまってるんだな、これ
ts

```typescript
 const updateItemPosition = (item:any, position:paper.Point) => {
   let newItems:any[] = state.items.filter((x:any) => (x != item));
   item.position = position; //ダメ！
   newItems.push(item);
   set((state:any) => ({
     ...state, 
     items: newItems, 
   }));
 }
```

一見できるようになったが2回目のドラッグ時になぜか初期位置に新しい付箋が生成される...
> let newItems:any[] = state.items.filter((x:any) => (x != item));
このstateが直前の状態ではなく外のスコープの初期状態を見ている
これが正解:
ts

```typescript
 const updateItemPosition = (item:any, position:paper.Point) => {
    set((state:any) => {
      let newItems:any[] = state.items.filter((x:any) => (x != item));
      item = {...item, position: position};
      newItems.push(item);
      return {
        ...state, 
        items: newItems, 
      };
    });
  }
```

