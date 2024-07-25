<h1>Functional Components</h1>

- **What They Are:** Functional components are simple JavaScript functions that return HTML (using JSX) to display UI elements.
- **How They Work:** They take in data (called props) as arguments and return JSX to render UI.
- **When to Use:** When you need a simple component that just displays some data or UI without much logic.

```jsx
function Greeting(props) {
  return <h1>Hello, {props.name}!</h1>;
}
```

<h1>Class Components</h1>

- **What They Are:** Class components are more complex and are created using ES6 classes. They can have state and lifecycle methods.
- **How They Work:** They extend from React.Component and must have a render method that returns JSX.
- **When to Use:** When you need a component with state or lifecycle methods.

```jsx
class Greeting extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}!</h1>;
  }
}
```

<h1>Component Lifecycle</h1>

- **What It Is:** The component lifecycle refers to the series of events from the creation of a component to its removal from the DOM.

<h3>Lifecycle Phases:</h3>

1. **Mounting:** When the component is first added to the DOM.
   - `componentDidMount`: Runs after the component is added to the DOM. Good for fetching data.

2. **Updating:** When the component’s props or state change.
    - `componentDidUpdate`: Runs after the component’s updates are flushed to the DOM.

3. **Unmounting:** When the component is removed from the DOM
    - `componentWillUnmount`: Runs right before the component is removed. Good for cleanup (like removing timers).

<h3>Example of Lifecycle Methods in a Class Component:</h3>

```jsx
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = { date: new Date() };
  }

  componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }

  componentDidUpdate(prevProps, prevState) {
    // Runs after every update
  }

  componentWillUnmount() {
    clearInterval(this.timerID);
  }

  tick() {
    this.setState({
      date: new Date()
    });
  }

  render() {
    return (
      <div>
        <h1>It is {this.state.date.toLocaleTimeString()}.</h1>
      </div>
    );
  }
}
```

<h3>summary</h3>

- **Functional components** are simple functions that return UI elements.
- **Class components** are more complex and can hold state and lifecycle methods.
- **Component lifecycle** describes the phases a component goes through from creation to removal, with specific methods that run at each phase to handle setup, updates, and cleanup.