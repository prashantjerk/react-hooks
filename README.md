# React Hooks

Here, I'll try to explain mostly used react hooks with their syntax and common mistakes done by the users. Also, <b>feel free to add or modify</b> the documentaion.

In react, hooks were introduced since v16.8.0. They were introduced to make writing codes easily using react. We'll learn how they make things easier later on.

React functions starting with `use` are <i>Hooks.</i> There are several react hooks provided, we can use them based on our requirements, and we can also combine the existing hooks.

### Points to know

#### - call react hooks before the functional components or another hook

This means, hooks such as `useState`, `useEffect`, `useContext`, etc., can only be called at the top level of a functional component or inside another custom hook.

When using hooks, React relies on the order of the hooks to maintain the state of the component. Hooks must be called in the same order on every render of the component.

If you call a hook inside of a conditional statement, for example, it may not be called on every render of the component, which can lead to inconsistent behavior. Similarly, if you call a hook inside of a nested function, it may not be called in the same order on every render, which can also cause unexpected behavior.

To ensure that hooks work correctly, they must be called at the top level of the component or inside a custom hook, and they must be called in the same order on every render. This allows React to track the state of the component and ensure that it remains consistent throughout the component's lifecycle.

<i>Example 1:</i> ❌ Hooks called after the functional component (incorrect) ❌

```
import React, { useState } from 'react';

function MyComponent() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <h1>{count}</h1>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

function App() {
  return (
    <div>
      <MyComponent />
      {useState('Hello')} // calling useState after the component
    </div>
  );
}

export default App;
```

⚠️ It's fine if you don't understand what the above code does. The goal right now is to understand dos and don'ts of react hooks. ⚠️

In <i>Example 1,</i> using `{useState('Hello')}` after `MyComponent()` is not a correct place to call the hook `useState`.

<i>Example 2:</i> ✅ Hooks called before the functional component (correct) ✅

```
import React, { useState } from 'react';

function MyComponent() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <h1>{count}</h1>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

function App() {
  const [message, setMessage] = useState('Hello');

  return (
    <div>
      {message}
      <MyComponent />
    </div>
  );
}

export default App;

```

<i>Example 2</i> is the right way to do it. We are calling `useState` before the end of `MyComponent()`, which is allowed. This code will work as expected and render a message followed by the `MyComponent()`.

#### Now lets dive deep into different types of react hooks

Here are few commonly used react hooks and their use:

- `useState`: used for creating and updating state variables in functional components
- `useEffect`: used for managing side effects, such as fetching data or updating the DOM, in functional components
- `useContext`: used for accessing and updating context values in functional components
- `useReducer`: used for managing state in a more complex and structured way than useState, especially when dealing with multiple related state variables and actions
- `useCallback`: used for memoizing functions in functional components to optimize performance
- `useMemo`: used for memoizing values in functional components to optimize performance
- `useRef`: used for creating and accessing a mutable reference value in functional components, such as a reference to a DOM element
- `useLayoutEffect`: similar to `useEffect`, but runs synchronously after all DOM mutations, which can be useful for measuring the size and position of DOM elements
- `useImperativeHandle`: used for exposing a parent component's imperative API to its child component, such as for triggering a child component's method from the parent component
- `useDebugValue`: used for displaying custom labels and values in the React DevTools when debugging components that use hooks.

⚠️ During this documentation, React hooks are not available for class components. It is possible that they may become available in the future. ⚠️

## `useState`

<u>Lets learn about this hook by the help of its syntax:</u>

<i>Example 3:</i>

```
import React, { useState } from 'react';

function MyComponent() {
 // Declare a state variable using the useState hook
 const [stateVariable, setStateVariable] = useState(initialState);

 // create a function
 return (
   <div>
     <p>The value of my state variable is: {stateVariable}</p>
   </div>
 );
}
```

In the <i>Example 3,</i> you can see we've imported `useState` from `React` as the hook is provided by react.js library. This is a basic program which shows what the syntax of `useState` looks like. As you can see, there are two different variables used for the purpose of state management: `stateVariable` and `setStateVariable`.

Here, `stateVariable` stores the current value of the state, and `setStateVariable` is the function which is responsible for updating the state. and inside the `useState()` we insert the initial value.

Later on we can use the value of current state anywhere we want, as used here using `{stateVariable}`

<hr>

<i>Example 4:</i>

<u>Lets see an example to be more clear:</u>

```
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  const handleClick = () => {
    setCount(count + 1);
  };

  return (
    <div>
      <p>You clicked the button {count} times.</p>
      <button onClick={handleClick}>Click me</button>
    </div>
  );
}
```
In this <i>Example 4,</i> we're using the `useState` hook to declare a state variable called `count` with an initial value of 0. We're also using the `setCount` function to update the value of count i.e. increasing by 1.

We're then rendering the current value of count in a paragraph element and a button that, when clicked, calls the `handleClick` function to update the value of `count` using `setCount`.

Whenever `setCount` is called, React will re-render the component with the updated value of `count`.

Here, all you need to understand is about the current value: `count`, initial value: `0` and the value-updating-function: `setCount` which updates the value present inside `count`. 