---
title: "scikit-image"
---

python

```
from skimage import io
import numpy as np
WIDTH = 400
HEIGHT = 300
data = [np.random.choice([0, 1], size=WIDTH)]
RULE30 = [0, 1, 1, 1, 1, 0, 0, 0]
for y in range(1, HEIGHT):
    prev = data[-1]
    next = [
        RULE30[prev[x - 1] * 4 + prev[x] * 2 + prev[x + 1 - 400]]
        for x in range(WIDTH)]
    data.append(next)
data = np.array(data)
io.imsave("tmp.png", data)
```

![image](https://gyazo.com/a045307e009597a1789ad92411ac7c8b/thumb/1000)

python

```
from skimage import io
import numpy as np
image = np.random.random((300, 400, 3))
io.imsave("tmp.png", image)
```

![image](https://gyazo.com/63e163e421d9f82d22c8d4f62c67bedd/thumb/1000)

python

```
from skimage import filters
from skimage import io
import numpy as np

WIDTH = 400
HEIGHT = 300
data = np.zeros((HEIGHT, WIDTH, 3))

for i in range(20):
    data[i * 10, i * 20] = (10 * i, 0, 0)
    data[i * 10 + 50, i * 20] = (0, 20 * i, 0)
    data[i * 10 + 100, i * 20] = (0, 0, 30 * i)
data = filters.gaussian(data, sigma=5, multichannel=True)

data *= 25
data *= 255
data = data.astype(np.uint8)
io.imsave("tmp.png", data)
```


![image](https://gyazo.com/fd994dca770c20d10ba49e4c59f1f788/thumb/1000)
