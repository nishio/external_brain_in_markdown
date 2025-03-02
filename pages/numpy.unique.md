---
title: "numpy.unique"
---

python

```
>>> set(np.int64("1 2 3 1 4 2 0".split()))
{0, 1, 2, 3, 4}
>>> np.unique(np.int64("1 2 3 1 4 2 0".split()))
array([0, 1, 2, 3, 4])
```

setがハッシュテーブルであるのに対し、こちらはソート済みのnp.arrayである
[https://numpy.org/doc/stable/reference/generated/numpy.unique.html](https://numpy.org/doc/stable/reference/generated/numpy.unique.html)

[[numpy.searchsorted]]で[[二分探索]]できる
> This function uses the same algorithm as the builtin python [[bisect]].bisect_left (side='left') and bisect.bisect_right (side='right') functions, which is also vectorized in the v argument.
[https://numpy.org/doc/stable/reference/generated/numpy.searchsorted.html](https://numpy.org/doc/stable/reference/generated/numpy.searchsorted.html)

[[numpy]]
