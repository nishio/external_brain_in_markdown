---
title: "Minecraft Variable"
---

MyCommand
console

```
> mycmd-variables create foo
[16:34:08 INFO]: MyCmd> Variable foo created.
> mycmd-variables set foo 0
[16:34:30 INFO]: Variable foo updated
[16:34:30 INFO]: New content for foo : 0.0
> mycmd-variables add foo 1
[16:35:06 INFO]: Variable foo updated
[16:35:06 INFO]: New value for foo : 1.0
> mycmd-variables add foo 1
[16:35:08 INFO]: Variable foo updated
[16:35:08 INFO]: New value for foo : 2.0
```


:

```
test:
  command: /test
  type: RUN_COMMAND
  runcmd:
    - "/say foo"
```


:

```
> mycmd-reload commands
> test
[16:38:39 INFO]: [Server] 2
```


:

```
test:
  command: /test
  type: RUN_COMMAND
  runcmd:
    - $Script$%Variable%foo+1
    - "/say foo"
    - $Script$%if%foo>5
    - $Script$%Variable%foo=0
```

