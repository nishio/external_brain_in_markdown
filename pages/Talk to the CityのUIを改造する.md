---
title: "Talk to the CityのUIを改造する"
---

`visualization.py`を見るとわかるように`command = f"REPORT={output_dir} npm run build"`をsubprocessで叩いているだけ

visualizationの手前のaggregationのstepで、可視化に必要なデータを全部result.jsonに集約している。
`next-app/pages/index.tsx`でそれを読んでいる
index.tsx

```
export async function getStaticProps({ params }: any) {
  const report = process.env.REPORT
  if (report && report.length) {
    const fs = require('fs');
    const result = fs.readFileSync(`../pipeline/outputs/${report}/result.json`, 'utf8');
    return { props: { result: JSON.parse(result) } }
  }
  const fs = require('fs');
  const subfolders = fs.readdirSync(outputs, { withFileTypes: true })
    .map((x: any) => x.name)
    .filter((x: string) => !x.startsWith('.'));
  return { props: { subfolders } };
}
```


この`{ props: { result: JSON.parse(result) } }`の部分がHTMLにはこんな感じで埋め込まれている

html

```html
    <script id="__NEXT_DATA__" type="application/json">
      {
        "props": {
          "pageProps": {
            "result": {
              "clusters": [
                {
                  "cluster": "環境配慮都市", ...
```

というわけで`"result": { ... }`のところをresult.jsonに書き出してやれば静的HTMLにしたレポートをベースに発展的なUI開発ができる

書き出したresult.jsonを仮に`scatter/pipeline/outputs/tokyo/result.json`においたとすると
`scatter/next-app%`で`$ REPORT=tokyo npm run build`すると`scatter/pipeline/outputs/tokyo/report/`に出力される

とりあえず検索ハイライトをつけてみた
- [[Talk to the City検索ハイライト機能]]


(`npm run dev`でホットリロードの開発サーバが起動することを期待したが `Error: Cannot find module 'react/jsx-runtime'`とエラーになって、よくわからないので諦めた)


