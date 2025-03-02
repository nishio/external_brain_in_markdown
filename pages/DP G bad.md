
from [[DP G]]
DP_G bad
- PyPy 15TLE
python

```
def solve(N, M, edges):
    path = edges.copy()
    exists = 1
    for i in range(2, M + 1):
        next_path = defaultdict(set)
        for v1 in path:
            for v2 in path[v1]:
                if edges[v2]:
                    next_path[v1].update(edges[v2])
                    exists = i
        if exists != i:
            # no more pathes
            break
        path = next_path
    return exists
```

