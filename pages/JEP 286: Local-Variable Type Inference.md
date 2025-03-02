---
title: "JEP 286: Local-Variable Type Inference"
---

[JEP 286: Local-Variable Type Inference](https://openjdk.org/jeps/286)

java

```
var list = new ArrayList<String>();  // infers ArrayList<String>
var stream = list.stream();          // infers Stream<String>
```

released in [[Java 10]]
- March 20, 2018
