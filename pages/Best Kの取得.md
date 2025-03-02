
from [[heapq]]
Best Kの取得
- サイズがkを超えたらpop
python

```
from random import shuffle
xs = list(range(100))
shuffle(xs)
K = 3
queue = xs[:K]
heapify(queue)
for x in xs[K:]:
    heappush(queue, x)
    heappop(queue)
print(queue)  # => [97, 98, 99]
```


