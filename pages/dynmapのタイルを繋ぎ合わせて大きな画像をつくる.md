
[[マイクラ]]の[[dynmap]]が生成するマップタイルを一つの画像に結合したい。
今まではdynmapの画面を開いてスクリーンショットを撮っていたが、cronで自動的に日付をつけて保存したいのでスクリプトを書く。

![image](https://gyazo.com/9a4bbeaf9294c91a928f480b5fc64753/thumb/1000)
python

```
import numpy as np
import skimage.util
import skimage.io

images = []
for x in reversed(range(32)):
    for y in range(32):
        image = skimage.io.imread(f'/opt/minecraft_server/plugins/dynmap/web/tiles/world/t/0_0/{y}_{x}.jpg/')
        images.append(image)

out = skimage.util.montage(images, grid_shape=(32, 32), multichannel=True)
skimage.io.imsave('out.jpg', out)
```

できた

違う場所もつくる
![image](https://gyazo.com/996417bb9053e75bc9aa86cbddb9719c/thumb/1000)
py

```
import numpy as np
import skimage.util
import skimage.io

TILE_DIR = "/opt/minecraft_server/plugins/dynmap/web/tiles"
world = "world"
cx = 0
cy = 1

images = []
for x in reversed(range(32)):
    for y in range(32):
        gx = cx * 32 + x
        gy = cy * 32 + y
        image = skimage.io.imread(f'{TILE_DIR}/{world}/t/{cy}_{cx}/{gy}_{gx}.jpg/')
        images.append(image)

out = skimage.util.montage(images, grid_shape=(32, 32), multichannel=True)
skimage.io.imsave('out.jpg', out)
```

チャンクだと思ってcxって名前にしたけどそういうわけではないみたいだな、チャンクは16単位だから。

人手でのスクリーンショットではなくタイルの結合なので並びるとピッタリつながる
- (PCで見ると並んでる、スマホだと横幅が足りないので改行されて見える)
![image](https://gyazo.com/9a4bbeaf9294c91a928f480b5fc64753/thumb/1000)![image](https://gyazo.com/996417bb9053e75bc9aa86cbddb9719c/thumb/1000)

あとはこれを日時付きで保存するようにしてcronで起動する
py

```
#!/home/nishio/venv/bin/python

import numpy as np
import skimage.util
import skimage.io
import time
# settings
TILE_DIR = "/opt/minecraft_server/plugins/dynmap/web/tiles"
OUT_DIR = "/home/nishio/dynmap_concat"
world = "world"
tx = 0
ty = 1
targets = [[0, 0], [0, 1]]
# end settings
today = time.strftime("%Y-%m-%d")

for [tx, ty] in targets:
    images = []
    for x in reversed(range(32)):
        for y in range(32):
            gx = tx * 32 + x
            gy = ty * 32 + y
            image = skimage.io.imread(f'{TILE_DIR}/{world}/t/{ty}_{tx}/{gy}_{gx}.jpg/')
            images.append(image)
    out = skimage.util.montage(images, grid_shape=(32, 32), multichannel=True)
    skimage.io.imsave(f'{OUT_DIR}/{tx}_{ty}_{today}.jpg', out)
```


TODO ある程度溜まったら繋げてタイムラプス動画にする
