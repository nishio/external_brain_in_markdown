
![image](https://gyazo.com/227e09f357758240a4f0893a56c42161/thumb/1000)
元ネタ
- 新世紀エヴァンゲリオンに登場する敵
- [https://evangelion.fandom.com/wiki/Leliel](https://evangelion.fandom.com/wiki/Leliel)
- > レリエルは東京3区の上空に突如現れた、白と黒の歪んだ色彩パターンを持つ浮遊球体に見える。しかし、レリエルの実体は、実は地上に現れた影のようなものである。我々の次元でのレリエルの肉体は、幅680メートル、厚さ3ナノメートルであり、球体はその「影」に過ぎないのである。

基本方針
- きれいな素材画像があるのでこれを元データにしてプログラムで生成する
    - ![image](https://gyazo.com/c310b7f3146c6cb0dfd69dd38f99d85c/thumb/1000)
    - [https://evangelion.fandom.com/wiki/Leliel](https://evangelion.fandom.com/wiki/Leliel)
- 視点と配置する座標からそれを投影した時の二次元上の点を求める
    - 素材画像から色を取得する
    - [[mcpi]]でブロックを配置

python

```
import numpy as np
import skimage.io
from mcpi import minecraft
from math import sqrt

# viewpoint
vp = np.array([6009.50, 80.00 + 1.5, 2.50])
# target
tp = np.array([6110, 150, -80])

cam_y = tp - vp
cam_y = cam_y / np.linalg.norm(cam_y)
cam_x = np.cross(cam_y, np.array([0, 1, 0]))
cam_x = cam_x / np.linalg.norm(cam_x)
cam_z = np.cross(cam_x, cam_y)

image = skimage.io.imread(f'/Users/nishio/Documents/leliel.png')
assert image.shape == (400, 400, 4)


def get_color(x, y, z):
    tp = np.array([x, y, z])
    d = tp - vp
    scale = 4.5
    down = np.dot(d, cam_z) * -scale + 200
    left = np.dot(d, cam_x) * scale + 200
    rgba = image[int(down), int(left)]
    if rgba[3] == 0:
        raise RuntimeError("transparent")
    if rgba[0] < 128:
        return BLACK
    return WHITE


RADIUS = 40
m = minecraft.Minecraft.create(HOST, PORT)
cx, cy, cz = tp
WOOL = 35
WHITE = 0
BLACK = 15
THICKNESS = 1.74  # larger than sqrt(3)
x, y, z = tp
for dx in range(-RADIUS, RADIUS + 1):
    x = cx + dx
    for dy in range(-RADIUS, RADIUS + 1):
        y = cy + dy
        for dz in range(-RADIUS, RADIUS + 1):
            z = cz + dz
            if abs(RADIUS - sqrt(dx ** 2 + dy ** 2 + dz ** 2)) < THICKNESS:
                m.setBlock([x, y, z, WOOL, get_color(x, y, z)])
```


マイクラ世界の球体に対して2次元画像を投影してる
- ![image](https://gyazo.com/cfc9f423a4014242cc891598d13acbd8/thumb/1000)
まがまがしいわ
- ![image](https://gyazo.com/ed7f2a433cd7ee8ca641dd1596bf98dd/thumb/1000)
世界が闇に覆われる
- ![image](https://gyazo.com/d2289d068169d7ee7720699dbca93a39/thumb/1000)


[https://youtu.be/2ZsXJLJb6uI](https://youtu.be/2ZsXJLJb6uI)

書き換えがどれくらいの時間でできるかわかる
- 面白いのでガンガン書き換える動画撮影を作ろうかと思ったけど原作を確認したらどちらかというと書き変わるのではなくゆっくり動いて、それからいきなり上空に来る感じだった
