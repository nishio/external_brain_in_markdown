
see Github
[https://github.com/nishio/tutorial-webworker-with-react/blob/master/README.md](https://github.com/nishio/tutorial-webworker-with-react/blob/master/README.md)




---draft
create react app
`$ npx create-react-app tutorial-webworker-with-react --typescript`

install worker-loader
`$ cd tutorial-webworker-with-react/`
`$ npm install worker-loader --save-dev`

add a heavy task
ts

```typescript
export const heavyTask = (target: string) => {
  console.log("hello,", target);
  const startTime = Date.now();
  while (Date.now() - startTime < 3000) {}
  console.log("bye,", target);
  return 42;
};
```


see the heavy task blocks UI

add webworker
ts

```typescript
import { heavyTask } from "./common";

onmessage = (e: any) => {
  const result = heavyTask("webworker");
  // @ts-ignore
  postMessage(result);
};
```


Unless @ts-ignore, I saw following error:
:

```
function postMessage(message: any, targetOrigin: string, transfer?: Transferable[] | undefined): void
Expected 2-3 arguments, but got 1.ts(2554)
lib.dom.d.ts(19636, 44): An argument for 'targetOrigin' was not provided.
```


Add button to call webworker
ts

```typescript
// eslint-disable-next-line import/no-webpack-loader-syntax
import Worker from "worker-loader!./webworker";

export const runOnWebWorker = (e: any) => {
  status = "running...";
  const worker = new Worker();
  worker.postMessage("heavyTask");
  worker.onmessage = function(event: any) {
    status = "finished";
  };
};
...
<button onClick={runOnWebWorker}>on WebWorker</button>
```


It works. But you may see following error:
:

```
Cannot find module 'worker-loader!./webworker'.
```

To fix it...

Add custom type definition


