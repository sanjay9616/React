<h1>Error Handling</h1>

Error handling in React involves capturing and managing errors that occur in the rendering process, lifecycle methods, and event handlers of components. React provides mechanisms for handling errors in both class and functional components.

<h1>Error Boundaries</h1>

Error boundaries are React components that catch JavaScript errors anywhere in their child component tree, log those errors, and display a fallback UI instead of crashing the whole component tree. Error boundaries are implemented using class components.

**1. Creating an Error Boundary:**

```jsx
import React, { Component } from 'react';

class ErrorBoundary extends Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    // Update state so the next render will show the fallback UI.
    return { hasError: true };
  }

  componentDidCatch(error, errorInfo) {
    // You can also log the error to an error reporting service
    console.log(error, errorInfo);
  }

  render() {
    if (this.state.hasError) {
      // You can render any custom fallback UI
      return <h1>Something went wrong.</h1>;
    }

    return this.props.children;
  }
}

export default ErrorBoundary;
```

**2. Using an Error Boundary:**

```jsx
import React from 'react';
import ErrorBoundary from './ErrorBoundary';
import MyComponent from './MyComponent';

const App = () => (
  <div>
    <h1>My App</h1>
    <ErrorBoundary>
      <MyComponent />
    </ErrorBoundary>
  </div>
);

export default App;
```

<h1>Handling Errors in Functional Components</h1>

Functional components can handle errors using hooks such as `useEffect` and `try-catch` blocks. Since functional components do not support lifecycle methods like class components, they rely on these hooks for side effects and error handling.

```jsx
import React, { useState, useEffect } from 'react';

const MyComponent = () => {
  const [data, setData] = useState(null);
  const [error, setError] = useState(null);

  useEffect(() => {
    const fetchData = async () => {
      try {
        const response = await fetch('https://api.example.com/data');
        if (!response.ok) {
          throw new Error('Network response was not ok');
        }
        const result = await response.json();
        setData(result);
      } catch (error) {
        setError(error.message);
      }
    };

    fetchData();
  }, []);

  if (error) {
    return <div>Error: {error}</div>;
  }

  if (!data) {
    return <div>Loading...</div>;
  }

  return (
    <div>
      <h1>Data</h1>
      <pre>{JSON.stringify(data, null, 2)}</pre>
    </div>
  );
};

export default MyComponent;
```

<h1>Explanation</h1>

**1. Error Boundaries:**

- Error boundaries are components that catch errors in their child component tree.
- They are implemented using class components.
- The `getDerivedStateFromError` method updates the state to show a fallback UI.
- The `componentDidCatch` method logs the error.

**2. Handling Errors in Functional Components:**

Use `useEffect` to handle side effects and fetch data.
Use `try-catch` blocks within `useEffect` to catch and handle errors.
Manage error state using the `useState` hook.

<h1>Summary</h1>

- **Error Boundaries:** Use class components to catch and handle errors in the component tree, providing a fallback UI.
- **Handling Errors in Functional Components:** Use hooks like `useEffect` and `useState` along with `try-catch blocks` to manage errors in functional components.

<h2><a href="https://github.com/sanjay9616/React/blob/main/README.md"> 🔙 Back</a></h2>
