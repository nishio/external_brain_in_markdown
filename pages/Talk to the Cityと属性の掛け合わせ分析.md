---
title: "Talk to the Cityと属性の掛け合わせ分析"
---

[[Talk to the City]]で自由記述データの分布を二次元可視化した上で、特定の属性(例えば年齢層、データソース、アンケートなら自由記述以外の選択肢質問の回答など)と掛け合わせて分析したいというニーズがある

この分析にはいくつもやり方がある
- 属性によってデータを分割してそれぞれ二次元可視化する
- まとめて二次元可視化したあと、属性によってハイライト/表示変更をする
それぞれメリットデメリットがあるが究極的には「やってみて観察するべき」であり、前者はデータを分けるだけで簡単だからここでは後者の解説を書く

可視化のためのデータは`result.json`にまとめられていて`index.tsx`の`getStaticProps`で読んでいる
なので可視化前に`result.json`を編集して属性のデータを追加するのが良いと思う
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

たとえばこう
result.json

```json
{
  "clusters": [ ... ],
  "comments": [ ... ],
  "propertyMap": {
    "年齢層": {
      "arg1": "20代",
      "arg2": "60代"
    },
    "データソース": {
      "arg1": "X",
      "arg2": "郵送"
    },
  }
}
```


実際の散布図は`DesktopMap.tsx`や`MobileMap.tsx`で下記のように実装されている
DesktopMap.tsx

```
{/* DOT CIRCLES */}
{clusters.map((cluster) =>
  cluster.arguments
    .filter(voteFilter.filter)
    .map(({ arg_id, x, y }) => (
      <circle
        className="pointer-events-none"
        key={arg_id}
        id={arg_id}
        cx={zoom.zoomX(scaleX(x) + 20)}
        cy={zoom.zoomY(scaleY(y))}
        fill={color(cluster.cluster_id, onlyCluster)}
        opacity={
          expanded && tooltip?.arg_id !== arg_id ? 0.3 : 1
        }
        r={tooltip?.arg_id === arg_id ? 8 : 4}
      />
    ))
)}
```


このcolor関数はpropsとしてコンポーネントの外部から与えられているが、引数としてcluster_idを取るようになっているので今のままではクラスタで塗ることしかできなくて都合が悪い。これを`arg_id`も取るようにすれば与える関数を変えて属性による色変えができるようになる
(onlyClusterは個別のクラスタを解説するところのビューのためにあるが、今後の拡張を考えるとこういう位置引数ではなくオプショナル変数にした方がいいかもね)
(個人的にはopacityもセットで返す関数にして「色はクラスター配色のまま、注目してない属性データ点は透明度を高くする」などができるようにしたいところだが話がややこしくなるので今回はパス)

このcolorは`Report.tsx`の中で`useClusterColor`というカスタムフックで指定している
`const color = useClusterColor(clusters.map((c) => c.cluster_id));`
属性ごとの掛け合わせ分析のビューを新しく追加するのか、このビューに掛け合わせ機能を追加するのかによって詳しい実装は変わるが、基本的にはこれをクラスターによる色付けに限定しないように変えて
`const [color, setColor] = useState(cluster_color)  // デフォルト値としてクラスタでの色付けにしている`
属性`attr`の選択をするUIで選択イベントのハンドラで
`setColor(color_by_attribute(attr))`
などとやればよい
`color_by_attribute(attr)`は「arg_idを引数にとってそのargumentのattr属性の値をみて色を決める関数」を返す関数
