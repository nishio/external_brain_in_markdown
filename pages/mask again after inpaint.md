
py

```
import numpy as np
from PIL import Image

init_image = Image.open("init_image.png")
mask_image = Image.open("mask_image.png")
cat_image = Image.open("cat_on_bench.png")

m = np.array(mask_image) / 255.0
bg = np.array(init_image) * (1 - m)
fg = np.array(cat_image) * m
img = bg + fg
img = img.astype(np.uint8)
Image.fromarray(img, "RGB").save("out.png")
```


![image](https://gyazo.com/1a38c6deac8fb1c7e78035413fa868a9/thumb/1000)
