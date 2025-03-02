---
title: "requestsでJSONをPOST"
---

python

```
payload = {"q": sample_text}
r = requests.post(API_URL, json=payload)
```

上記のコードで良い
- 下記でも同様に動く。よく使うのでショートカットが用意されてる
- 日本語を含む文字列なのでエンコードする必要があるかと思ったが、それはJSONにする際に内部的に行われるので自分でやる必要はない
    - むしろ、やるとbytesがJSON compatibleでないので `TypeError: Object of type bytes is not JSON serializable` になる

python

```
payload = json.dumps({"q": sample_text})
headers = {'content-type': 'application/json'}
r = requests.post(API_URL, data=payload, headers=headers)
```

