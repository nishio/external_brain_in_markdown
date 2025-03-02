---
title: "cannot compile namespaces when the '--isolatedModules' flag is provided"
---

- [[React]] [[TypeScript]]
- [[create-react-app]]した時に自動で'--isolatedModules'フラグがつく
- 新しいtsファイルを作成した時にこのエラーが出るようになる
- これはこのファイルが何もexportしてないため
    - モジュールとして適切でなく、たんなるnamespaces
    - エラーメッセージがわかりにくい

対処法
typescript

```typescript
let Foo;
export default Foo;
```

とか書いておくととりあえずモジュールとして適切な形になる。
あとで正しい「エクスポートすべきもの」ができてから差し替える。
