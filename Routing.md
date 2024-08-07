<h1>React Router Basics</h1>

React Router is a standard library for routing in React. It enables navigation among views of various components, allows changing the browser URL, and keeps the UI in sync with the URL.

**1. Installation:** `npm install react-router-dom`

**2. Basic Setup:**

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';

const Home = () => <h2>Home</h2>;
const About = () => <h2>About</h2>;
const Contact = () => <h2>Contact</h2>;

const App = () => (
  <Router>
    <Switch>
      <Route exact path="/" component={Home} />
      <Route path="/about" component={About} />
      <Route path="/contact" component={Contact} />
    </Switch>
  </Router>
);

ReactDOM.render(<App />, document.getElementById('root'));
```

<h1>Dynamic Routing and Nested Routes</h1>

Dynamic routing refers to routes that can change based on user actions or other factors.

**1. Dynamic Routes:**

```jsx
const User = ({ match }) => <h2>User ID: {match.params.id}</h2>;

const App = () => (
  <Router>
    <Switch>
      <Route exact path="/" component={Home} />
      <Route path="/user/:id" component={User} />
    </Switch>
  </Router>
);
```

**2. Nested Routes:**

```jsx
const Topics = ({ match }) => (
  <div>
    <h2>Topics</h2>
    <ul>
      <li>
        <Link to={`${match.url}/components`}>Components</Link>
      </li>
      <li>
        <Link to={`${match.url}/props-v-state`}>Props v. State</Link>
      </li>
    </ul>

    <Route path={`${match.path}/:topicId`} component={Topic} />
  </div>
);

const Topic = ({ match }) => <h3>Requested Topic ID: {match.params.topicId}</h3>;

const App = () => (
  <Router>
    <Switch>
      <Route exact path="/" component={Home} />
      <Route path="/topics" component={Topics} />
    </Switch>
  </Router>
);
```

<h1>URL Parameters and Query Strings</h1>

**1. URL Parameters:**

URL parameters are part of the URL path that can be accessed in the component via `match.params`.

```jsx
const Product = ({ match }) => <h2>Product ID: {match.params.productId}</h2>;

const App = () => (
  <Router>
    <Switch>
      <Route path="/product/:productId" component={Product} />
    </Switch>
  </Router>
);
```

**2. Query Strings:**

Query strings are parts of the URL that follow the `?` symbol and can be accessed using the `useLocation` hook from `react-router-dom`.

```jsx
import { useLocation } from 'react-router-dom';

const useQuery = () => {
  return new URLSearchParams(useLocation().search);
};

const Products = () => {
  let query = useQuery();
  return <h2>Filter: {query.get('filter')}</h2>;
};

const App = () => (
  <Router>
    <Switch>
      <Route path="/products" component={Products} />
    </Switch>
  </Router>
);
```

<h1>Putting It All Together</h1>

Here's a comprehensive example incorporating all the concepts:

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import { BrowserRouter as Router, Route, Switch, Link, useLocation } from 'react-router-dom';

// Components
const Home = () => <h2>Home</h2>;
const About = () => <h2>About</h2>;
const Contact = () => <h2>Contact</h2>;
const User = ({ match }) => <h2>User ID: {match.params.id}</h2>;
const Topic = ({ match }) => <h3>Requested Topic ID: {match.params.topicId}</h3>;

// Helper Hook
const useQuery = () => {
  return new URLSearchParams(useLocation().search);
};

const Products = () => {
  let query = useQuery();
  return <h2>Filter: {query.get('filter')}</h2>;
};

// Nested Routes
const Topics = ({ match }) => (
  <div>
    <h2>Topics</h2>
    <ul>
      <li>
        <Link to={`${match.url}/components`}>Components</Link>
      </li>
      <li>
        <Link to={`${match.url}/props-v-state`}>Props v. State</Link>
      </li>
    </ul>

    <Route path={`${match.path}/:topicId`} component={Topic} />
  </div>
);

// Main App
const App = () => (
  <Router>
    <div>
      <nav>
        <ul>
          <li>
            <Link to="/">Home</Link>
          </li>
          <li>
            <Link to="/about">About</Link>
          </li>
          <li>
            <Link to="/contact">Contact</Link>
          </li>
          <li>
            <Link to="/user/123">User 123</Link>
          </li>
          <li>
            <Link to="/topics">Topics</Link>
          </li>
          <li>
            <Link to="/products?filter=popular">Products</Link>
          </li>
        </ul>
      </nav>

      <Switch>
        <Route exact path="/" component={Home} />
        <Route path="/about" component={About} />
        <Route path="/contact" component={Contact} />
        <Route path="/user/:id" component={User} />
        <Route path="/topics" component={Topics} />
        <Route path="/products" component={Products} />
      </Switch>
    </div>
  </Router>
);

ReactDOM.render(<App />, document.getElementById('root'));
```

This setup demonstrates React Router basics, dynamic routing, nested routes, URL parameters, and query strings in a cohesive application.

<h2><a href="https://github.com/sanjay9616/React/blob/main/README.md"> 🔙 Back</a></h2>
