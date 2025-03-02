---
title: "クラスのインスタンスをspreadしてもメソッドは複製されない"
---

ts

```typescript
class Greeter {
  greeting: string;

  constructor(message: string) {
    this.greeting = message;
  }

  greet() {
    return "Hello, " + this.greeting;
  }
}

const x: Greeter = new Greeter("world");
const y: Greeter = { ...x };
// Property 'greet' is missing in type '{ greeting: string; }' but required in type 'Greeter'.
```

[[TypeScript]]
