# React 18

## Breaking Changes
One of the changes you can make is to alter ```render``` to ```createRoot```
```
// Before
import { render } from "react-dom";
 
const container = document.getElementById("app");
render(<App tab="home" />, container);
 
// After
import { createRoot } from "react-dom/client";
 
const container = document.getElementById("app");
const root = createRoot(container);
root.render(<App tab="home" />);
```
```createRoot``` enables concurrent features from React 18. To ensure you migrate your app properly, try enabling strict mode. Strict mode will let you know what is happening with components in development, and it will print out any irregularities in the console.

```
import React from "react";
import { createRoot } from "react-dom/client";
 
function App() {
  return (
    <div>
      <Header />
      <React.StrictMode>
        <div>
          <Content />
          <SignUpForm />
        </div>
      </React.StrictMode>
      <Footer />
    </div>
  );
}
 
const container = document.getElementById("app");
const root = createRoot(container);
root.render(<App />);
```

## React Hooks

Hooks were first introduced in React 16.8. Hooks helps us to manage our component's state, or performing an after effect when certain changes occur in state(s) without writing a class.

## useState Hook

The state of our application is bound to change at some point. This could be the value of a variable, an object, or whatever type of data exists in our component.

To make it possible to have the changes reflected in the DOM, we have to use a React hook called ```useState```.

```
import { useState } from "react";

function App() {
  const [name, setName] = useState("Ihechikara");
  const changeName = () => {
    setName("Chikara");
  };

  return (
    <div>
      <p>My name is {name}</p>
      <button onClick={changeName}> Click me </button>
    </div>
  );
}

export default App;
```

Also, if you're using hydrate for server-side rendering with hydration, you can upgrade to hydrateRoot:

````
// Before
import { hydrate } from "react-dom";
const container = document.getElementById("app");
hydrate(<App tab="home" />, container);
 
// After
import { hydrateRoot } from "react-dom/client";
const container = document.getElementById("app");
const root = hydrateRoot(container, <App tab="home" />);
// Unlike with createRoot, you don't need a separate root.render() call here.
```