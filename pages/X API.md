---
title: "X API"
---

- [[X APIのレートリミット]]
- [[X APIの費用]]
- Q: X APIのAPI KeyとAPI Key Secretがある、Bearer Tokenはどうしたら得られる？
sh

```
curl -u 'API_KEY:API_KEY_SECRET' \
     --data 'grant_type=client_credentials' \
     'https://api.x.com/oauth2/token'
```


