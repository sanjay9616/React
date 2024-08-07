<h1>Code Splitting</h1>

Code splitting is a technique that allows you to split your code into smaller bundles, which can then be loaded on demand or in parallel. This improves the initial load time of your application by only loading the necessary code for the current view.

<h1>Lazy Loading Components</h1>

Lazy loading in React allows you to load components only when they are needed. This can significantly reduce the initial load time of your application by splitting the code into smaller chunks.

<h3>Using React.lazy and Suspense:</h3>

```jsx
import React, { Suspense, lazy } from 'react';

// Lazy load the component
const LazyComponent = lazy(() => import('./LazyComponent'));

const App = () => {
  return (
    <div>
      <h1>Welcome to My App</h1>
      <Suspense fallback={<div>Loading...</div>}>
        <LazyComponent />
      </Suspense>
    </div>
  );
};

export default App;
```
```jsx
// LazyComponent.js
import React from 'react';

const LazyComponent = () => {
  return <div>This is a lazily loaded component!</div>;
};

export default LazyComponent;
```

- **React.lazy:** The React.lazy function lets you define a component that is loaded dynamically. The argument to React.lazy is a function that returns a promise for a module, which should have a default export containing the React component.
- **Suspense:** Suspense is a component that can be used to wrap the lazy-loaded component. The fallback prop takes a React element that is shown while the component is being loaded.

<h3>React Suspense</h3>

`React.Suspense` is used to handle the loading state of one or more lazy-loaded components. It can display a fallback while waiting for the lazy-loaded component to load.

```jsx
import React, { Suspense, lazy } from 'react';

const LazyComponentA = lazy(() => import('./LazyComponentA'));
const LazyComponentB = lazy(() => import('./LazyComponentB'));

const App = () => {
  return (
    <div>
      <h1>Welcome to My App</h1>
      <Suspense fallback={<div>Loading components...</div>}>
        <LazyComponentA />
        <LazyComponentB />
      </Suspense>
    </div>
  );
};

export default App;
```
```jsx
// LazyComponentA.js
import React from 'react';

const LazyComponentA = () => {
  return <div>This is Lazy Component A!</div>;
};

export default LazyComponentA;
```
```jsx
// LazyComponentB.js
import React from 'react';

const LazyComponentB = () => {
  return <div>This is Lazy Component B!</div>;
};

export default LazyComponentB;
```

- **Multiple Lazy-Loaded Components:** This example shows how you can use Suspense to handle the loading state of multiple lazy-loaded components. The fallback is displayed until both LazyComponentA and LazyComponentB are loaded.

<h1>Summary</h1>

- **Code Splitting:** Divides your code into smaller chunks that can be loaded on demand.
- **Lazy Loading:** Loads components only when they are needed using React.lazy.
- **React Suspense:** Manages the loading state of lazy-loaded components with a fallback UI.

These techniques help improve the performance of your React application by reducing the initial load time and loading resources as needed.

<h2><a href="https://github.com/sanjay9616/React/blob/main/README.md"> 🔙 Back</a></h2>