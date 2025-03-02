---
title: "JSからFlaskを叩いて400 Bad Request"
---

"Content-Type": "application/json"で叩いてるのにFlaskの側でrequest.dataで受けて400 Bad Requestになった
request.jsonを使う

full sample:
ts

```typescript
const data = { user: "test", talk: "test", text: text };
fetch("https://keicho.herokuapp.com/api/web/", {
  mode: "cors",
  method: "POST",
  body: JSON.stringify(data),
  headers: {
    "Content-Type": "application/json",
  },
}).then((response) => {
  console.log(response);
});
```

python

```
@app.route('/api/web/', methods=["POST"])
def web_api():
    user = request.json.get("user")
    talk = request.json.get("talk")
    text = request.json["text"]
    return keicho.connect_web(user, talk, text)
```

