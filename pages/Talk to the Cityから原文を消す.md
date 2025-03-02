---
title: "Talk to the Cityから原文を消す"
---

[[Talk to the City]]から原文を消す
![image](https://gyazo.com/a9c1e423b0e8b549a8aff2be124a2f1a/thumb/1000)

Talk to the Cityでは点をクリックすると原文が表示される
![image](https://gyazo.com/a29a8db4850f02678f17a4d8e890e2be/thumb/1000) ![image](https://gyazo.com/ca98459215468c0d5d2f550aa5f15bb8/thumb/1000)
しかし原文表示のために全データが埋め込まれていることでレポート画面が重くなる問題があるし、原文の送信可能化権の許諾がないなどの理由で原文を表示したくないケースがある
- なお法律に詳しい人と話して、僕が当初思っていたのより広い範囲で「引用」と主張できそうとわかった
- 関連: [[公表されたものは引用できる]]

# UIからの削除
[https://github.com/AIObjectives/talk-to-the-city-reports/blob/main/scatter/next-app/components/Tooltip.tsx#L67-L87](https://github.com/AIObjectives/talk-to-the-city-reports/blob/main/scatter/next-app/components/Tooltip.tsx#L67-L87)
ts

```typescript
    {expanded ? <div>
      <VideoLink {...point} showVideo={true} showThumbnail={false} />
      <div className='text-sm opacity-80 mt-2'>
        <span className='font-semibold'>{t(point.video ? "Transcript" : "Original comment")}:</span>
        "{point.comment.length > 100 && !showMoreComment ?
          <span>
            {point.comment.slice(0, 200) + '..."'}
            <span className='underline cursor-pointer'
              onClick={() => setShowMoreComment(true)}>
              {t("read more")}
            </span>
          </span> :
          point.comment + '"'}
      </div>
      <div className='text-xs opacity-50 italic mt-4'>
        {t("Click anywhere on the map to close this")}
      </div>
    </div> :
      <div className='text-xs opacity-50 italic'>
        {t(point.video ? "Click on the dot to see original video and transcript" : "Click on the dot for details")}
      </div>}
```

この範囲をコメントアウトすればUIからは消せる(静的コンテンツの再生成が必要)
- `$ main.py -o visualization config/...`


# データからも消す
でもデータからも消したいよね(無駄に重くなるし)

データ型はこんな感じ
ts

```typescript
export type Argument = {
  arg_id: string;
  argument: string;
  comment_id: string;
  x: number;
  y: number;
  p: number;
};

export type CommentObj = {
  comment: string;
  agrees?: number;
  disagrees?: number;
  video?: string;
  interview?: string;
  timestamp?: string;
};

export type CommentsMap = {
  [id: string]: CommentObj;
};
...
export type Point = Argument & Cluster & CommentObj & { color: string };
```


データをどこで読んでるかというと
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


分析実行環境の出力のresult.jsonを読んでサーバサイドレンダリングで静的HTMLにしている

静的HTML生成済みのものから消す場合
このデータは静的出力後は`_next/data`以下にある
![image](https://gyazo.com/6c72e29ea71539ec1686a21f0eee4f96/thumb/1000)

![image](https://gyazo.com/56a9864d1b189b4cf5206955bdbd4a40/thumb/1000)
これを空にしよう

# comment空文字化処理
python

```
import json
filename = "_next/data/8gQb47OhoAQvRNCBqVMIF/index.json"
```

python

```
data = json.load(open(filename))
comments = data["pageProps"]["result"]["comments"]
for k in comments:
    comments[k]["comment"] = ""
json.dump(data, open(filename, "w"), ensure_ascii=False) 
```


![image](https://gyazo.com/0345f756f553ce9f41743b2553461be7/thumb/1000)
消せました

しかしこれだけではWeb画面から消えなかった
なぜかと思ったらそもそもindex.htmlに全部埋め込まれていた(index.jsonは何のためにある？読まれてる？)
![image](https://gyazo.com/f4e5228d3f59ed8ce46fc4f27dbd5264/thumb/1000)
json

```json
{"props": ...,"page":"/","query":{},"buildId":"aZQl6X8wn0bor6WDO4T50","assetPrefix":".","isFallback":false,"gsp":true,"scriptLoader":[]}
```

の...の部分にindex.jsonの内容が埋め込まれている
ここの内容をcomment空文字化処理済みのindex.jsonの中身で置き換えれば

![image](https://gyazo.com/6ae6643dffe9fb2b2c8c887a8cb04400/thumb/1000)
データからも消えたことが確認されました

UI再生成をする場合
visualizationの手前でJSONから消すのが良いと思う
