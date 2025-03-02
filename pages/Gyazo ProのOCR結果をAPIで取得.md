
python

```
import requests

GYAZO_API_TOKEN = "..."
GYAZO_API_ROOT = "https://api.gyazo.com/api"
GYAZO_IMAGE_ID = "bf881c1e44d798978431f9a2af02acdb"

res = requests.get(
    f"{GYAZO_API_ROOT}/images/{GYAZO_IMAGE_ID}", headers={
        "Authorization": f"Bearer {GYAZO_API_TOKEN}"
    }
)
print(res.json()["ocr"]["description"])
```


PyPIに[[python-gyazo]]ってのはあるけど、単独画像のID指定での取得が未実装で、しかもレスポンスの"ocr"は無視されちゃうので結構手を入れないとこの目的に使えず、上記の通り数行で目的が達成できるから使う必要がなかった
[https://github.com/ymyzk/python-gyazo/blob/master/gyazo/api.py](https://github.com/ymyzk/python-gyazo/blob/master/gyazo/api.py)

[[OCR]]
[[Gyazo API]]
