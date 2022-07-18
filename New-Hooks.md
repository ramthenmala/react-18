# 5 New Hooks in React 18

## 1. useId

```useId``` is a new hook for generating unique IDs on both the client and server, while avoiding hydration mismatches.

```
function CodeOfConductField() {
  const id = useId();
 
  return (
    <>
      <label htmlFor={id}>Do you agree with our Code of Conduct?</label>
      <input id={id} type="checkbox" name="coc" />
    </>
  );
}
```

## 1. useTransition