
[[React Hooks]] [Hooks API Reference – React](https://reactjs.org/docs/hooks-reference.html#usereducer)
js

```javascript
const [state, dispatch] = useReducer(reducer, initialArg, init);
```


- [[Redux]]

An alternative to useState.
js

```javascript
const [state, setState] = useState(initialState);
```

Accepts a reducer of type `(state, action) => newState`
returns the current state paired with a dispatch method.

useReducer is usually preferable to useState
- when you have complex state logic
    - that involves multiple sub-values or
- when the next state depends on the previous one.

useReducer also lets you optimize performance for components
- that trigger deep updates
- because you can pass dispatch down instead of callbacks.

Here’s the counter example from the useState section, rewritten to use a reducer:

js

```javascript
const initialState = {count: 0};

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return {count: state.count + 1};
    case 'decrement':
      return {count: state.count - 1};
    default:
      throw new Error();
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);
  return (
    <>
      Count: {state.count}
      <button onClick={() => dispatch({type: 'increment'})}>+</button>
      <button onClick={() => dispatch({type: 'decrement'})}>-</button>
    </>
  );
}
```


setState版
js

```javascript
function Counter({initialCount}) {
  const [count, setCount] = useState(initialCount);
  return (
    <>
      Count: {count}
      <button onClick={() => setCount(initialCount)}>Reset</button>
      <button onClick={() => setCount(prevCount => prevCount + 1)}>+</button>
      <button onClick={() => setCount(prevCount => prevCount - 1)}>-</button>
    </>
  );
}
```


React guarantees that dispatch function identity is stable and won’t change on re-renders. This is why it’s safe to omit from the useEffect or useCallback dependency list.

Specifying the initial state
There’s two different ways to initialize useReducer state. You may choose either one depending on the use case. The simplest way to pass the initial state as a second argument:

    - const [[state, dispatch]] = useReducer(
            - reducer,
            - {count: initialCount}
    - );
Note

React doesn’t use the state = initialState argument convention popularized by Redux. The initial value sometimes needs to depend on props and so is specified from the Hook call instead. If you feel strongly about this, you can call useReducer(reducer, undefined, reducer) to emulate the Redux behavior, but it’s not encouraged.

Lazy initialization
You can also create the initial state lazily. To do this, you can pass an init function as the third argument. The initial state will be set to init(initialArg).

It lets you extract the logic for calculating the initial state outside the reducer. This is also handy for resetting the state later in response to an action:
js

```javascript
function init(initialCount) {
  return {count: initialCount};
}

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return {count: state.count + 1};
    case 'decrement':
      return {count: state.count - 1};
    case 'reset':
      return init(action.payload);
    default:
      throw new Error();
  }
}

function Counter({initialCount}) {
  const [state, dispatch] = useReducer(reducer, initialCount, init);
  return (
    <>
      Count: {state.count}
      <button
        onClick={() => dispatch({type: 'reset', payload: initialCount})}>

        Reset
      </button>
      <button onClick={() => dispatch({type: 'increment'})}>+</button>
      <button onClick={() => dispatch({type: 'decrement'})}>-</button>
    </>
  );
}
```


Bailing out of a dispatch
If you return the same value from a Reducer Hook as the current state, React will bail out without rendering the children or firing effects. (React uses the Object.is comparison algorithm.)

Note that React may still need to render that specific component again before bailing out. That shouldn’t be a concern because React won’t unnecessarily go “deeper” into the tree. If you’re doing expensive calculations while rendering, you can optimize them with [[useMemo]].

[useReducerフック活用法 - Qiita](https://qiita.com/ossan-engineer/items/1192c224e4252ec0f421)
[React hooksを基礎から理解する (useReducer編) - Qiita](https://qiita.com/seira/items/2fbad56e84bda885c84c)
