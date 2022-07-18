# Automatic Batching in React 18

Automatic batching means that React will now batch updates inside components. Batching prevents unnecessary renders of component.

In React 17, if we change the state of the component two times, the component will re-render two times. Now, in React 18, the two updates will be batched, and the component will render only once. And that's only if you're using createRoot instead of render.

[Demo](https://codesandbox.io/s/morning-sun-lgz88?file=/src/index.js)
```
// Before: only React events were batched
setTimeout(() => {
  setSize((oldSize) => oldSize + 1);
  setOpen((oldOpen) => !oldOpen);
  // React will render twice, once for each state update (no batching)
}, 1000);
 
// After: updates inside of timeouts, promises,
// native event handlers or any other event are batched
setTimeout(() => {
  setSize((oldSize) => oldSize + 1);
  setOpen((oldOpen) => !oldOpen);
  // React will only re-render once at the end (that is batching)
}, 1000);
```

If automatic batching is not something not want in your component, we can always opt-out with ```flushSync```.

```
import { flushSync } from "react-dom"; // Note: we are importing from react-dom, not react
 
function handleSubmit() {
  flushSync(() => {
    setSize((oldSize) => oldSize + 1);
  });
 
  // React has updated the DOM by now
  flushSync(() => {
    setOpen((oldOpen) => !oldOpen);
  });
 
  // React has updated the DOM by now
}
```