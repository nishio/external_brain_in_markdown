
from [[Jestメモ]]
setTimeoutをPromiseで包む

before
ts

```typescript
export function sendToServer(text: string) {
  if (...) {
    ...
  } else {
    // bot is sleeping
    setTimeout(() => {
      sendToServer(text);
    }, 1000);
  }
}
```


after
ts

```typescript
export function sendToServer(text: string) {
  if (...) {
    ...
  } else {
    return new Promise((resolve) => setTimeout(resolve, 1000)).then(() => {
      sendToServer(text, newLogs);
    });
  }
} 
```

