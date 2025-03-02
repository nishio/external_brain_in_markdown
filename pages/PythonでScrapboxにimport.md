---
title: "PythonでScrapboxにimport"
---

Puppeteerを使えばScrapboxにボットを住まわせられることがわかったのでNodeとPuppeteerを勉強しよう
→NodeとPuppeteerを勉強してるしてる間にPuppeteerが必要なくなってたw
→Puppeteerいらないならぼく不慣れなNode使わずにPythonでできるのでは…試してみるか
→できた

python

```
import requests
from dotenv import load_dotenv
import json
import os

load_dotenv()

API_ME = "https://scrapbox.io/api/users/me"
API_IMPORT = "https://scrapbox.io/api/page-data/import/{project}.json"


def write_pages(pages):
    sid = os.getenv("SID")
    project = os.getenv("PROJECT")

    cookie = "connect.sid=" + sid
    r = requests.get(API_ME, headers={"Cookie": cookie})
    r.raise_for_status()
    csrfToken = r.json()["csrfToken"]

    url = API_IMPORT.format(project=project)
    data = json.dumps({"pages": pages})
    r = requests.post(
        url,
        files={"import-file": data},
        headers={
            "Cookie": cookie,
            "Accept": "application/json, text/plain, */*",
            "X-CSRF-TOKEN": csrfToken,
        }
    )
    r.raise_for_status()


def _test():
    pages = [
        {
            "title": "Scbot Home",
            "lines": ["Scbot Home", "Hello world!"]
        }
    ]
    write_pages(pages)
```

[https://github.com/nishio/scbot/blob/0.1/t.py](https://github.com/nishio/scbot/blob/0.1/t.py)
