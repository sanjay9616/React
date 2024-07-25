<h1>Passing Data to Components</h1>

<h3>Passing Data from Parent to Child</h3>

- **What It Is:** Passing data from a parent component to a child component via props.
- **How It Works:** The parent component passes data to the child component as attributes in the JSX.

```jsx
// Parent Component
function Parent() {
  const parentData = "Hello from Parent";
  return <Child data={parentData} />;
}

// Child Component
function Child(props) {
  return <h1>{props.data}</h1>;
}
```

<h3>Passing Data from Child to Parent</h3>

- **What It Is:** Passing data from a child component to a parent component using callback functions.
- **How It Works:** The parent component provides a function as a prop to the child. The child component calls this function to send data back to the parent.

```jsx
// Parent Component
function Parent() {
  const handleDataFromChild = (childData) => {
    console.log(childData); // Logs: "Hello from Child"
  };

  return <Child sendData={handleDataFromChild} />;
}

// Child Component
function Child(props) {
  const childData = "Hello from Child";
  return <button onClick={() => props.sendData(childData)}>Send Data to Parent</button>;
}
```

<h3>Passing Data to a Component with No Direct Relationship</h3>

- **What It Is:** Sharing data between components that do not have a direct parent-child relationship.
- **How It Works:** Use a shared state management solution like Context API or a state management library (e.g., Redux) to share data across the component tree.

```jsx
import React, { createContext, useContext, useState } from 'react';

// Create a Context
const DataContext = createContext();

// Parent Component
function App() {
  const [sharedData, setSharedData] = useState("Hello from Context");

  return (
    <DataContext.Provider value={sharedData}>
      <ComponentA />
      <ComponentB />
    </DataContext.Provider>
  );
}

// Component A (which has no direct relation to Component B)
function ComponentA() {
  const data = useContext(DataContext);
  return <h1>Component A: {data}</h1>;
}

// Component B (which has no direct relation to Component A)
function ComponentB() {
  const data = useContext(DataContext);
  return <h1>Component B: {data}</h1>;
}
```

<h1>Prop Types and Default Props</h1>

<h3>Prop Types</h3>

- This is a way to specify the expected types of props that a component should receive. It helps catch bugs by ensuring that the props passed to a component are of the correct type.
- **How to Use:** Use the prop-types library to define the types of props.

```jsx
import PropTypes from 'prop-types';

function Greeting(props) {
  return <h1>Hello, {props.name}!</h1>;
}

Greeting.propTypes = {
  name: PropTypes.string.isRequired,
  age: PropTypes.number,
};
```
- **Explanation:** Here, name must be a string and is required, while age can be a number but is optional.

<h3>Default Props</h3>

- This is a way to set default values for props if they are not provided by the parent component.
- **How to Use:** Define default props directly on the component.

```jsx
function Greeting(props) {
  return <h1>Hello, {props.name}!</h1>;
}

Greeting.defaultProps = {
  name: 'Guest',
};
```

<h3>Combined Example with Prop Types and Default Props</h3>

```jsx
import PropTypes from 'prop-types';

function Greeting(props) {
  return (
    <div>
      <h1>Hello, {props.name}!</h1>
      {props.age && <p>Your age is {props.age}.</p>}
    </div>
  );
}

Greeting.propTypes = {
  name: PropTypes.string.isRequired,
  age: PropTypes.number,
};

Greeting.defaultProps = {
  name: 'Guest',
};

// Usage
function App() {
  return (
    <div>
      <Greeting name="Alice" age={25} />
      <Greeting /> {/* This will use the default prop for name */}
    </div>
  );
}
```