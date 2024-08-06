<h1>State Management in React</h1>

State management in React involves handling the state of components and ensuring data flows correctly throughout the application. There are several approaches to managing state in React, including lifting state up, using state management libraries like Redux, MobX, and Recoil.

<h1>Lifting State Up</h1>

Lifting state up refers to moving the state to the nearest common ancestor of the components that need to share the state. This approach ensures that the state is managed in a single place and can be passed down to child components as props.

```jsx
import React, { useState } from 'react';

const ChildA = ({ value, onChange }) => (
  <div>
    <h2>Child A</h2>
    <input type="text" value={value} onChange={(e) => onChange(e.target.value)} />
  </div>
);

const ChildB = ({ value }) => (
  <div>
    <h2>Child B</h2>
    <p>{value}</p>
  </div>
);

const Parent = () => {
  const [sharedValue, setSharedValue] = useState('');

  return (
    <div>
      <ChildA value={sharedValue} onChange={setSharedValue} />
      <ChildB value={sharedValue} />
    </div>
  );
};

export default Parent;
```

<h1>Redux</h1>

Redux is a predictable state container for JavaScript apps, often used with React. It helps manage the application state in a single, central store.

```jsx
// actions.js
export const increment = () => ({ type: 'INCREMENT' });
export const decrement = () => ({ type: 'DECREMENT' });

// reducer.js
const initialState = { count: 0 };

const counterReducer = (state = initialState, action) => {
  switch (action.type) {
    case 'INCREMENT':
      return { count: state.count + 1 };
    case 'DECREMENT':
      return { count: state.count - 1 };
    default:
      return state;
  }
};

export default counterReducer;

// store.js
import { createStore } from 'redux';
import counterReducer from './reducer';

const store = createStore(counterReducer);

export default store;

// App.js
import React from 'react';
import { Provider, useSelector, useDispatch } from 'react-redux';
import store from './store';
import { increment, decrement } from './actions';

const Counter = () => {
  const count = useSelector((state) => state.count);
  const dispatch = useDispatch();

  return (
    <div>
      <h2>Count: {count}</h2>
      <button onClick={() => dispatch(increment())}>Increment</button>
      <button onClick={() => dispatch(decrement())}>Decrement</button>
    </div>
  );
};

const App = () => (
  <Provider store={store}>
    <Counter />
  </Provider>
);

export default App;
```

<h1>MobX</h1>

MobX is a state management library that makes state management simple and scalable by using observables.

```jsx
// store.js
import { makeAutoObservable } from 'mobx';

class CounterStore {
  count = 0;

  constructor() {
    makeAutoObservable(this);
  }

  increment() {
    this.count++;
  }

  decrement() {
    this.count--;
  }
}

const counterStore = new CounterStore();
export default counterStore;

// App.js
import React from 'react';
import { observer } from 'mobx-react';
import counterStore from './store';

const Counter = observer(() => {
  return (
    <div>
      <h2>Count: {counterStore.count}</h2>
      <button onClick={() => counterStore.increment()}>Increment</button>
      <button onClick={() => counterStore.decrement()}>Decrement</button>
    </div>
  );
});

const App = () => (
  <div>
    <Counter />
  </div>
);

export default App;
```

<h1>Recoil</h1>

Recoil is a state management library for React that provides a way to share state between components and manage global state in a more flexible way.

```jsx
// atoms.js
import { atom } from 'recoil';

export const counterState = atom({
  key: 'counterState', // unique ID (with respect to other atoms/selectors)
  default: 0, // default value (aka initial value)
});

// App.js
import React from 'react';
import { RecoilRoot, useRecoilState } from 'recoil';
import { counterState } from './atoms';

const Counter = () => {
  const [count, setCount] = useRecoilState(counterState);

  return (
    <div>
      <h2>Count: {count}</h2>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <button onClick={() => setCount(count - 1)}>Decrement</button>
    </div>
  );
};

const App = () => (
  <RecoilRoot>
    <Counter />
  </RecoilRoot>
);

export default App;
```

<h1>Summary</h1>

- **Lifting State Up:** Moving state to the nearest common ancestor of components that need to share it.
- **Redux:** A predictable state container for JavaScript apps, often used with React.
- **MobX:** A state management library that uses observables to make state management simple and scalable.
- **Recoil:** A state management library for React that provides flexible state sharing and management.