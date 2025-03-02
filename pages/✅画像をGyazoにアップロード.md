---
title: "✅画像をGyazoにアップロード"
---

python

```
def upload_to_gyazo(asin):
    local_filename = f"gyazo_cache/{asin}.txt"
    if os.path.isfile(local_filename):
        return open(local_filename).read()

    url = 'https://upload.gyazo.com/upload.cgi'
    image_filaname = f"image_cache/{asin}.jpg"
    files = {'imagedata': (image_filaname, open(image_filaname, "rb").read())}
    r = requests.post(url, files=files)
    open(local_filename, "w").write(r.text)
    return r.text
```


追記
- Gyazoへのアップロードがエラーになった時にエラーメッセージがキャッシュに書かれるのを直した方が良い
画像を[[Gyazo]]にアップロード
[[Gyazo API]]
