---
title: "Adobe XDでSVGアイコンを作る"
---

[[Adobe XD]]で[[SVG]]アイコンを作る
- 選択範囲のエクスポートができる
- グループ化して1つにしておく
    - グループ化しないで複数個選んでると名前の指定なしにオブジェクト名を使って個別に出力されるため
- 目的サイズの白い縁のない箱を作っておいて配列ツールで中央揃えしてグループ化すると良い
    - 単にエクスポートするとバウンディングボックスのサイズで出力される
    - 後からサイズや配置を調整するのは面倒

![image](https://gyazo.com/a16b20bf64b060534600631a7621ac17/thumb/1000)

SVGなのでプログラムでスタイルを変えるのも簡単。Reactコンポーネントにした

ts

```typescript
export const LassoSVGButton = (props: any) => {
  const strokecolor = isActive(window.app.paperLassoTool) ? "#00C" : "#777";
  const strokewidth = isActive(window.app.paperLassoTool) ? "3" : "1";
  return (
    <svg onClick={props.onClick} viewBox="0 0 50 50">
      <rect x="5" y="5" width="40" height="40" rx="10"
        fill="none" stroke={strokecolor} stroke-width={strokewidth} stroke-dasharray="5 2"/>
    </svg>
  )
}
```



