---
title: "rsyncでマイクラを差分バックアップ"
---

丸ごとコピーしてバックアップ取ると同じファイルが何度もコピーされて非効率
rsyncで変更されてないファイルをハードリンクにする
- [rsyncで差分バックアップを行うための「--link-dest」オプション：Command Technica - ITmedia エンタープライズ](https://www.itmedia.co.jp/enterprise/articles/0804/25/news034.html)

通常のバックアップでは訪問済みのリージョンをすべてコピーするが、この方法なら更新したリージョンだけがコピーされるので容量節約かつ高速化する

2021-11-19
- Pythonにする
- `--exclude-from=FILE     read exclude patterns from FILE`
- `$ du -d 3 . | sort -nr`

2021-10-25
bash

```
rsync -a --delete --link-dest=../`ls | grep "backup" | tail -n1` minecraft_server backup`TZ=Asia/Tokyo date +%Y%m%d_%H%M`
```


解説
- backup`TZ=Asia/Tokyo date +%Y%m%d_%H%M`
    - 現在時刻を元に`backup20211025_1624`みたいなファイル名を作る
- `ls | grep "backup" | tail -n1`
    - backupを含むファイル名のうち最後のものを取得


rsyncのオプションのメモ
:

```
-a, --archive               archive mode; equals -rlptgoD (no -H,-A,-X)
-r, --recursive             recurse into directories
-l, --links                 copy symlinks as symlinks
-p, --perms                 preserve permissions
-t, --times                 preserve modification times
-g, --group                 preserve group
-o, --owner                 preserve owner (super-user only)
-D                          same as --devices --specials
    --devices               preserve device files (super-user only)
    --specials              preserve special files
```


[[マイクラ]]

差分にする前に使っていたPythonスクリプト
python

```
import shutil
from datetime import datetime 

IGNORE = """
.git
jdk*
*.jar
logs
block-backups
.archive-unpack
*.tar
""".strip().splitlines()

now = datetime.now().strftime("%Y%m%d_%H%M")

shutil.copytree(
    "minecraft_server", 
    f"backup{now}",
    ignore=shutil.ignore_patterns(*IGNORE),
)
```

