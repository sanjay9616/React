<h1>Context API</h1>

The Context API in React is used for managing state globally. It allows you to share values between components without having to pass props manually at every level of the tree. This is especially useful for themes, user authentication, and other data that needs to be accessible across many components.

<h3>Creating and Using Context</h3>

**1. Creating Context:**

- You create a context using the createContext function from React.

```jsx
import React, { createContext, useState, useContext } from 'react';

const MyContext = createContext();
```

**2. Creating a Context Provider:**

- The context provider is used to wrap the components that need access to the context values. It uses the `Provider` component and passes the value via the `value` prop.

```jsx
const MyProvider = ({ children }) => {
  const [state, setState] = useState('Initial Value');

  return (
    <MyContext.Provider value={{ state, setState }}>
      {children}
    </MyContext.Provider>
  );
};
```

**3. Consuming Context:**

- You can consume context in any component that is wrapped by the provider using the useContext hook.

```jsx
const MyComponent = () => {
  const { state, setState } = useContext(MyContext);

  return (
    <div>
      <p>{state}</p>
      <button onClick={() => setState('New Value')}>Change Value</button>
    </div>
  );
};
```

**Example**

Here's a complete example demonstrating how to create and use context in a simple React application:

```jsx
import React, { createContext, useState, useContext } from 'react';
import ReactDOM from 'react-dom';

// Create a context
const MyContext = createContext();

// Create a provider component
const MyProvider = ({ children }) => {
  const [state, setState] = useState('Initial Value');

  return (
    <MyContext.Provider value={{ state, setState }}>
      {children}
    </MyContext.Provider>
  );
};

// Create a consumer component
const MyComponent = () => {
  const { state, setState } = useContext(MyContext);

  return (
    <div>
      <p>{state}</p>
      <button onClick={() => setState('New Value')}>Change Value</button>
    </div>
  );
};

// Use the provider to wrap the application
const App = () => (
  <MyProvider>
    <MyComponent />
  </MyProvider>
);

ReactDOM.render(<App />, document.getElementById('root'));
```

<h3>Context Provider and Consumer</h3>

**Provider:**

- The `Provider` component is part of the context object created with `createContext`. It allows consuming components to subscribe to context changes.
- The `value` prop of the `Provider` is where you pass the data you want to share.

```jsx
<MyContext.Provider value={{ state, setState }}>
  {children}
</MyContext.Provider>
```

**Consumer:**

- The Consumer component or the useContext hook allows components to access the context values.

```jsx
const { state, setState } = useContext(MyContext);
```

This approach simplifies the state management process, making it easier to share data across multiple components without prop drilling.