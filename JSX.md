<h1>Syntax and Usage</h1>

JSX (JavaScript XML) is a syntax extension for JavaScript that looks similar to HTML. It is used in React to describe what the UI should look like. JSX makes it easy to write and visualize the structure of your UI components. Here’s a breakdown of the syntax and how to use JSX:

<h3>1. Basic Syntax:</h3>

- JSX elements are written within JavaScript code and look like HTML tags.
- Each JSX element can have attributes, children, and can be self-closing.

```jsx
const element = <h1>Hello, world!</h1>;
```

<h3>2. Embedding in JavaScript:</h3>

- JSX can be embedded in JavaScript expressions and assigned to variables, used in functions, etc.

```jsx
function Welcome() {
  return <h1>Hello, world!</h1>;
}
```

<h3>3. Attributes:</h3>

- JSX attributes are similar to HTML attributes, but they follow the camelCase naming convention for properties.

```jsx
const element = <img src="image.png" alt="Description" />;
```

<h3>4. Children:</h3>

- JSX elements can contain children, including other JSX elements.

```jsx
const element = (
  <div>
    <h1>Hello, world!</h1>
    <p>This is a paragraph.</p>
  </div>
);
```

<h3>5. Self-Closing Tags:</h3>

- If an element has no children, it can be self-closing.

```jsx
const element = <img src="image.png" alt="Description" />;
```

<h3>6. JavaScript Expressions:</h3>

- You can embed JavaScript expressions in JSX by wrapping them in curly braces `{}`.

```jsx
const name = 'John';
const element = <h1>Hello, {name}!</h1>;
```

<h1>Embedding Expressions</h1>

JSX allows you to embed any JavaScript expression within curly braces {}. This can be used for displaying variables, calling functions, or even evaluating expressions directly within your JSX.

<h3>1. Embedding Variables:</h3>

- You can embed variables in JSX to display their values

```jsx
const name = 'John';
const element = <h1>Hello, {name}!</h1>;
```

<h3>2. Expressions:</h3>

- You can include any JavaScript expression within curly braces.

```jsx
const number = 5;
const element = <p>The number is {number * 2}.</p>;
```

<h3>3. Function Calls:</h3>

- You can call functions and use their return values in JSX.

```jsx
function formatName(user) {
  return user.firstName + ' ' + user.lastName;
}

const user = {
  firstName: 'John',
  lastName: 'Doe'
};

const element = <h1>Hello, {formatName(user)}!</h1>;
```

<h3>4. Conditional Expressions:</h3>

- You can use ternary operators for conditional rendering.

```jsx
const isLoggedIn = true;
const element = <p>{isLoggedIn ? 'Welcome back!' : 'Please log in.'}</p>;
```

<h3>5. Inline Styling:</h3>

- You can embed objects for inline styling.

```jsx
const divStyle = {
  color: 'blue',
  backgroundColor: 'lightgray'
};

const element = <div style={divStyle}>Styled Text</div>;
```

<h3>Summary</h3>

JSX is a powerful syntax extension for JavaScript that makes writing React components more intuitive and readable. By allowing HTML-like syntax within JavaScript, JSX simplifies the creation of complex UI structures. Embedding expressions in JSX further enhances its flexibility, enabling dynamic content and interactivity within your components.

<h2><a href="https://github.com/sanjay9616/React/blob/main/README.md"> 🔙 Back</a></h2>

