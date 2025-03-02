
ts

```typescript
const onKeyPress: KeyboardEventHandler<HTMLTextAreaElement> = (e) => {
    // console.log(e.target.value)
    // Property 'value' does not exist on type 'EventTarget'
    // why?
    const target = e.target as HTMLTextAreaElement;
    console.log(target.value)
    // OK
}

```

