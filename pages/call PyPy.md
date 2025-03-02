
python

```
import subprocess
import sys
if sys.argv[-1] != "DONTCALL":
  subprocess.call("pypy3 Main.py DONTCALL", shell=True)
  sys.exit()
print("hello, pypy!")
```

[https://atcoder.jp/contests/abc177/submissions/16407994](https://atcoder.jp/contests/abc177/submissions/16407994)
