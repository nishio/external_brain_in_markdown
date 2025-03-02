---
title: "Facebook MessengerをJSONエクスポート"
---

公式の機能でJSONエクスポートができるようになったので、会話の内容をニーズに合わせて整形するのも簡単になった
- 設定>あなたのFacebook情報>個人データをダウンロード>「フォーマット: JSON」で「ファイルを作成」

python

```
from datetime import datetime
import json
data = json.load(open("inbox/XXXXXXXX/message_1.json"))

prev_date = ""
for m in reversed(data["messages"]):
    date = datetime.fromtimestamp(m['timestamp_ms'] // 1000)
    str_date = date.strftime("%Y-%m-%d")
    if str_date != prev_date:
        print(str_date)
        prev_date = str_date
    if "content" in m:
        sender = "T:"
        if m["sender_name"].startswith("Nishio"):
            sender = "N:"
        print(sender,
              m["content"].encode("latin-1").decode("utf-8"))
```


これに使った
[[キャリブレーション会]]

5行くらいCopilotが書いた
[https://twitter.com/nishio/status/1453992902279892993?s=21](https://twitter.com/nishio/status/1453992902279892993?s=21)
