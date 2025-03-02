---
title: "line_profiler"
---

`@profile`
`$ kernprof -l x.py `
`$ python3 -m line_profiler x.py.lprof > prof`
- "ValueError: source code string cannot contain null bytes"
    - `kernprof -l test.py` not `kernprof -l python test.py`
