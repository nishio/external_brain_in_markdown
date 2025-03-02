
[D - Knapsack 1](https://atcoder.jp/contests/dp/tasks/dp_d)
- 指定された制限重量以下で価値を最大化する問題
- [[ナップサック]]
- 重量を定義域とし、その重量での最大価値を値とするDP

- PyPy 166 ms
- `for j in range(W - weight + 1)`の+1を忘れて最大重量の場合を更新し忘れるミス
python

```
def solve(N, W, WV):
    values = [0] * (W + 1)
    for i in range(N):
        next_values = values[:]
        weight, value = WV[i]
        for j in range(W - weight + 1):
            next_values[j + weight] = max(
                values[j + weight],
                values[j] + value)
        values = next_values
    return max(values)
```

