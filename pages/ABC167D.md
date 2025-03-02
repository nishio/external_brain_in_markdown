---
title: "ABC167D"
---

python

```
def solve(N, K, xs):
    "void()"
    town_to_time = np.zeros(N, np.uint16)
    time_to_town = np.zeros(N, np.uint16)
    cur = 1
    for i in range(K):
        cur = xs[cur - 1]
        # print(town_to_time, time_to_town, cur)
        if town_to_time[cur - 1]:
            # visited before
            period = i + 1 - town_to_time[cur - 1]
            rest = K - i - 1
            rest %= period
            # print(rest, town_to_time[cur - 1], town_to_time[cur - 1] + rest)
            print(time_to_town[town_to_time[cur - 1] + rest - 1])
            return

        town_to_time[cur - 1] = i + 1
        time_to_town[i] = cur
    print(cur)
```


AC: 42, WA: 15, max_time: 0.34
np.uint16
np.uint32

AC
