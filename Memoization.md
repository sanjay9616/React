<h1>Memoization in React</h1>

Memoization in React is a performance optimization technique that prevents unnecessary re-renders of components by caching the result of expensive calculations. React provides several built-in hooks and higher-order components for memoization: `React.memo`, `useMemo`, and `useCallback`.

<h1>React.memo</h1>

`React.memo` is a higher-order component that memoizes a functional component. It prevents the component from re-rendering if its props have not changed.

```jsx
import React from 'react';

const ChildComponent = React.memo(({ name }) => {
  console.log('ChildComponent rendered');
  return <div>Hello, {name}!</div>;
});

const ParentComponent = () => {
  const [count, setCount] = React.useState(0);

  return (
    <div>
      <button onClick={() => setCount(count + 1)}>Increment Count</button>
      <p>Count: {count}</p>
      <ChildComponent name="John" />
    </div>
  );
};

export default ParentComponent;
```

In this example, `ChildComponent` only re-renders when its `name` prop changes. Clicking the button to increment the count does not cause `ChildComponent` to re-render, which is confirmed by the `console.log` statement.

<h1>useMemo</h1>

`useMemo` is a hook that memoizes the result of a calculation, recomputing it only when one of its dependencies changes. It is useful for avoiding expensive calculations on every render.

```jsx
import React, { useState, useMemo } from 'react';

const ExpensiveCalculationComponent = () => {
  const [count, setCount] = useState(0);
  const [text, setText] = useState('');

  const expensiveCalculation = (num) => {
    console.log('Expensive calculation');
    return num * 2;
  };

  const result = useMemo(() => expensiveCalculation(count), [count]);

  return (
    <div>
      <button onClick={() => setCount(count + 1)}>Increment Count</button>
      <p>Count: {count}</p>
      <p>Result: {result}</p>
      <input
        type="text"
        value={text}
        onChange={(e) => setText(e.target.value)}
        placeholder="Type something..."
      />
    </div>
  );
};

export default ExpensiveCalculationComponent;
```

In this example, the `expensiveCalculation` function is only called when `count` changes. Typing in the input field does not trigger the expensive calculation.

<h1>useCallback</h1>

`useCallback` is a hook that memoizes a callback function, preventing its recreation on every render. It is useful when passing callbacks to child components to avoid unnecessary re-renders.

```jsx
import React, { useState, useCallback } from 'react';

const ChildComponent = React.memo(({ onClick }) => {
  console.log('ChildComponent rendered');
  return <button onClick={onClick}>Click me</button>;
});

const ParentComponent = () => {
  const [count, setCount] = useState(0);

  const handleClick = useCallback(() => {
    console.log('Button clicked');
  }, []);

  return (
    <div>
      <button onClick={() => setCount(count + 1)}>Increment Count</button>
      <p>Count: {count}</p>
      <ChildComponent onClick={handleClick} />
    </div>
  );
};

export default ParentComponent;
```

In this example, the `handleClick` function is memoized using `useCallback`, preventing ChildComponent from re-rendering unnecessarily when `count` changes. The `ChildComponent` only re-renders if `handleClick` changes.

<h1>Summary</h1>

- **React.memo:** Memoizes functional components to prevent re-renders if props haven't changed.
- **useMemo:** Memoizes the result of an expensive calculation, recomputing it only when dependencies change.
- **useCallback:** Memoizes a callback function to prevent its recreation on every render, useful for passing stable callbacks to child components.

<h2><a href="https://github.com/sanjay9616/React/blob/main/README.md"> 🔙 Back</a></h2>


