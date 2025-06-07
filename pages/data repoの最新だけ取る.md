---
title: "data repoの最新だけ取る"
---

`$ git clone --depth 1 https://github.com/ORG/REPO.git`

GitHub Actions
taml

```
- uses: actions/checkout@v4
  with:
    fetch-depth: 1
```


`$ git pull --ff-only --depth=1`

[[data repo]]
