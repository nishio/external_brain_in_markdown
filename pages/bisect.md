
[[二分探索]]
「kを超える最初の場所」がright、「k以上の最初の場所」がleft
python

```
>>> import bisect
>>> xs = [1, 2, 4, 4, 5]
>>> [bisect.bisect_left(xs, x) for x in range(7)]
[0, 0, 1, 2, 2, 4, 5]
>>> [bisect.bisect_right(xs, x) for x in range(7)]
[0, 1, 2, 2, 4, 5, 5]
```

![image](https://gyazo.com/357c7b0a1c8a25f8bf415ae5bbc791fa/thumb/1000)

[[atcoder]]
