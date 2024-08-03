<h1>1. useState Hook in React</h1>

The `useState` hook is one of the most commonly used hooks in React. It allows you to add state to functional components, making them more powerful and flexible. Here’s a detailed breakdown of how it works and some examples to illustrate its usage.

**Importing useState**

```jsx
import React, { useState } from 'react';
```

**Basic Usage**

```jsx
const [state, setState] = useState(initialState);
```

**Example 1: Simple Counter**

```jsx
import React, { useState } from 'react';

const Counter = () => {
  const [count, setCount] = useState(0);

  const increment = () => {
    setCount(count + 1);
  };

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
    </div>
  );
};

export default Counter;
```

**Example 2: Form Input**

```jsx
import React, { useState } from 'react';

const Form = () => {
  const [name, setName] = useState('');

  const handleChange = (event) => {
    setName(event.target.value);
  };

  const handleSubmit = (event) => {
    event.preventDefault();
    alert(`Name submitted: ${name}`);
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Name:
        <input type="text" value={name} onChange={handleChange} />
      </label>
      <button type="submit">Submit</button>
    </form>
  );
};

export default Form;
```

**Example 3: Toggle Button**

```jsx
import React, { useState } from 'react';

const Toggle = () => {
  const [isOn, setIsOn] = useState(false);

  const toggle = () => {
    setIsOn(!isOn);
  };

  return (
    <div>
      <p>{isOn ? 'ON' : 'OFF'}</p>
      <button onClick={toggle}>Toggle</button>
    </div>
  );
};

export default Toggle;
```

**Example 4: Multiple State Variables**

```jsx
import React, { useState } from 'react';

const Profile = () => {
  const [name, setName] = useState('');
  const [age, setAge] = useState(0);
  const [email, setEmail] = useState('');

  const handleSubmit = (event) => {
    event.preventDefault();
    alert(`Name: ${name}, Age: ${age}, Email: ${email}`);
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Name:
        <input type="text" value={name} onChange={(e) => setName(e.target.value)} />
      </label>
      <label>
        Age:
        <input type="number" value={age} onChange={(e) => setAge(Number(e.target.value))} />
      </label>
      <label>
        Email:
        <input type="email" value={email} onChange={(e) => setEmail(e.target.value)} />
      </label>
      <button type="submit">Submit</button>
    </form>
  );
};

export default Profile;
```

**Summary:** The useState hook is essential for adding and managing state in React functional components. It simplifies state handling, making it easy to build dynamic and interactive UIs.

<h1>2. useEffect Hook in React</h1>

The `useEffect` hook allows you to perform side effects in functional components. It is a close replacement for lifecycle methods like `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount` in class components.

**Importing useEffect**

```jsx
import React, { useEffect } from 'react';
```

**Basic Usage**

```jsx
useEffect(() => {
  // Side effect logic here
}, [dependencies]);
```

**Example 1: Fetching Data on Component Mount**

This example demonstrates how to fetch data from an API when the component mounts.

```jsx
import React, { useState, useEffect } from 'react';

const DataFetcher = () => {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetch('https://api.example.com/data')
      .then(response => response.json())
      .then(data => setData(data));
  }, []); // Empty dependency array ensures this runs only once on mount

  return (
    <div>
      {data ? <pre>{JSON.stringify(data, null, 2)}</pre> : <p>Loading...</p>}
    </div>
  );
};

export default DataFetcher;
```

**Example 2: Setting up and Cleaning up a Timer**

This example shows how to set up a timer when the component mounts and clean it up when the component unmounts.

```jsx
import React, { useState, useEffect } from 'react';

const Timer = () => {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => {
      setSeconds(prevSeconds => prevSeconds + 1);
    }, 1000);

    return () => clearInterval(interval); // Cleanup function, to clear the interval
  }, []); // Empty dependency array ensures this runs only once on mount

  return (
    <div>
      <p>Seconds: {seconds}</p>
    </div>
  );
};

export default Timer;
```

**Example 3: Updating the Document Title**

This example updates the document title based on the component's state.

```jsx
import React, { useState, useEffect } from 'react';

const DocumentTitleUpdater = () => {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `Count: ${count}`;
  }, [count]); // Dependency array includes count, so this effect runs when count changes

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
};

export default DocumentTitleUpdater;
```

**Example 4: Fetch Data with Dependency**

This example demonstrates fetching new data whenever a dependency changes.

```jsx
import React, { useState, useEffect } from 'react';

const UserFetcher = ({ userId }) => {
  const [user, setUser] = useState(null);

  useEffect(() => {
    fetch(`https://api.example.com/users/${userId}`)
      .then(response => response.json())
      .then(data => setUser(data));
  }, [userId]); // Dependency array includes userId, so this effect runs when userId changes

  return (
    <div>
      {user ? <pre>{JSON.stringify(user, null, 2)}</pre> : <p>Loading...</p>}
    </div>
  );
};

export default UserFetcher;
```

**Summary:** The useEffect hook is powerful for managing side effects in React functional components. It allows you to perform actions like fetching data, setting up subscriptions, and manually changing the DOM. By specifying dependencies, you can control when the effect runs, making it a versatile tool for managing component lifecycle events.

<h1>3. useContext Hook in React</h1>

The `useContext` hook allows you to consume context in functional components, providing a way to share values like themes, user data, or settings across the component tree without passing props down manually at every level.

**Creating and Using a Context**

- Create a Context
- Provide the Context
- Consume the Context

**Step 1: Create a Context**

First, create a context using React.createContext.

```jsx
import React, { createContext, useState } from 'react';

// Create a Context
const ThemeContext = createContext();
```

**Step 2: Provide the Context**

Use a context provider to pass the current context value to the tree below.

```jsx
const ThemeProvider = ({ children }) => {
  const [theme, setTheme] = useState('light');

  return (
    <ThemeContext.Provider value={{ theme, setTheme }}>
      {children}
    </ThemeContext.Provider>
  );
};
```

**Step 3: Consume the Context**

Use `useContext` to consume the context value in any functional component.

```jsx
import React, { useContext } from 'react';

const ThemedComponent = () => {
  const { theme, setTheme } = useContext(ThemeContext);

  const toggleTheme = () => {
    setTheme(theme === 'light' ? 'dark' : 'light');
  };

  return (
    <div style={{ background: theme === 'light' ? '#fff' : '#333', color: theme === 'light' ? '#000' : '#fff' }}>
      <p>The current theme is {theme}</p>
      <button onClick={toggleTheme}>Toggle Theme</button>
    </div>
  );
};
```

**Putting It All Together**

Here's a complete example demonstrating how to create, provide, and consume a context in a simple React app.

```jsx
// App Component
import React from 'react';
import { ThemeProvider } from './ThemeProvider';
import ThemedComponent from './ThemedComponent';

const App = () => {
  return (
    <ThemeProvider>
      <ThemedComponent />
    </ThemeProvider>
  );
};

export default App;
```
```jsx
// ThemeProvider Component
import React, { createContext, useState } from 'react';

// Create a Context
const ThemeContext = createContext();

const ThemeProvider = ({ children }) => {
  const [theme, setTheme] = useState('light');

  return (
    <ThemeContext.Provider value={{ theme, setTheme }}>
      {children}
    </ThemeContext.Provider>
  );
};

export { ThemeProvider, ThemeContext };
```
```jsx
// ThemedComponent Component
import React, { useContext } from 'react';
import { ThemeContext } from './ThemeProvider';

const ThemedComponent = () => {
  const { theme, setTheme } = useContext(ThemeContext);

  const toggleTheme = () => {
    setTheme(theme === 'light' ? 'dark' : 'light');
  };

  return (
    <div style={{ background: theme === 'light' ? '#fff' : '#333', color: theme === 'light' ? '#000' : '#fff' }}>
      <p>The current theme is {theme}</p>
      <button onClick={toggleTheme}>Toggle Theme</button>
    </div>
  );
};

export default ThemedComponent;
```

**Summary:** The `useContext` hook simplifies the process of consuming context in functional components. It helps in managing global states efficiently without prop drilling, making the code more maintainable and clean.




