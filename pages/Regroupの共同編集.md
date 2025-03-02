---
title: "Regroupの共同編集"
---

Regroupで共同編集ツールがどうやって実現されてるのかの解説

ts

```typescript
ReactDOM.render(<Router />, document.getElementById('root'));
```


ts

```typescript
const Router = () => {
  return (
    <HashRouter>
      <Route path="/:id" component={WhenHashSpecified} />

      <Route exact path="/">
		...
      </Route>
    </HashRouter>
  );
}
```


ts

```typescript
function WhenHashSpecified(obj: any) {
  return (
    <App urlParam={obj.match.params.id} />
  );
}
```


ts

```typescript
const App = (props: { urlParam: string }) => { 
  useUrlParam(props.urlParam)
  ...
```


ts

```typescript
export const useUrlParam = (urlParam: string) => {
  useEffect(() => {
    // resolve map name
  	// subscribe changes on server
  	...
  }, [urlParam]);

  const items = getGlobal().items;
  useEffect(() => {
  	// save to server if items are changed
  }, [items]);
};
```


// save to server if items are changed
- マウスのドラッグで付箋の位置が動いた時に、各マウスムーブごとにリクエストが飛ぶともっさりするので100msごとにした
- 今は「そもそもマウスムーブごとにReact的状態の更新をするのも良くない」と考え直した
ts

```typescript
if (toSave) {
  // do nothing
} else {
  toSave = true;
  setTimeout(() => {
    toSave = false;
    saveToServer()
  }, 100)
}
```


// resolve map name
- URLパラメータを元に、参照すべきマップの名前を解決する。
- 最初に作ったときはマップを見るリンクで編集できて、その後で「編集できないけど閲覧できる」GoogleDocみたいなのを実現したくてこうなった。閲覧リンクから編集リンクを予想できない仕組み。
- エラー処理は雑、キーが見つからない場合は白紙のマップにファールバックする
- ここが「インターネットに接続してなかったらローカルのデータを表示」にしたい
ts

```typescript
if (urlParam.match(/key=([^&]*)/)) {
  const key = RegExp.$1;
  db.collection("key_to_map").doc(key).get().then((doc: any) => {
    if (doc.exists) {
      console.log("map exists")
      const toConnect = true;
      const { isReadOnly, mapname } = doc.data()
      setGlobal({
        toConnect: toConnect,
        isReadOnly: isReadOnly,
        mapname: mapname
      })
      setUpReadSubscription(toConnect, isReadOnly, mapname);
    } else {
      // doc.data() will be undefined in this case
      console.log("No such document!");
    }
  }).catch((error: any) => {
    console.log("Error getting document:", error);
  });
} else {
  // handle special case for development
} 
```


// subscribe changes on server
基本はこう
ts

```typescript
let unsubscribe = db.collection("map").doc(mapname).onSnapshot((doc: any) => {
  loadFromServer(doc.data());
});
```

書き込み可能な時には「サーバのデータを読む前に手元で変更して上書きしないように」という意図で、まず読み込んでからsubscribeしてるが、そもそも読み込みが完了するまで編集不能にすべき

マップの新規作成
- 初期状態をサーバに書き込んで新規タブで開いてる
- ネットワーク接続がない時にも新規作成したい
- しかしaddのcatchはすぐには呼ばれない、黙って内部でリトライされてしまうため
    - [[Firestoreでオフライン判定]]単体ではできない件も関係してそう
ts

```typescript
const createNewMap = () => {
  saveToNewMap(INITIAL_GLOBAL_STATE).then((docRef: any) => {
    window.open(`/#/key=${docRef.id}`)
  })
}
```

ts

```typescript
export const saveToNewMap = (state: TYPE_GLOBAL_STATE) => {
  const doc = convertStateToFirestore(state);
  return db.collection("map").add(doc)
    .then((docRef: any) => {
      return db.collection("key_to_map").add(
        { mapname: docRef.id }
      )
    })
    .catch((error: any) => {
      alert(`Error: ${error}`)
    });
}
```


