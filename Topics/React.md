# React<!-- omit in toc -->

React is an open source JavaScript library for building interactive user interfaces from small isolated pieces called components.

## Table of contents<!-- omit in toc -->

- [Official website](#official-website)
- [Setting up a new single page app](#setting-up-a-new-single-page-app)
- [React component templates](#react-component-templates)
  - [The index.jsx](#the-indexjsx)
  - [The app component](#the-app-component)
  - [Functional components](#functional-components)
  - [Class components](#class-components)
- [State](#state)
- [Props](#props)
- [Callback functions](#callback-functions)
- [Hooks](#hooks)
  - [Use state](#use-state)
  - [Use effect](#use-effect)
  - [Use ref](#use-ref)

## Official website

For more information see: <https://reactjs.org>.

## Setting up a new single page app

Navigate to your workspace and run:

```sh
npx create-react-app name
```

Then move into your project folder:

```sh
cd name
```

Start the localhost:3000 development server with:

```sh
npm start
```

## React component templates

### The index.jsx

React components are declared in `.jsx` files (or `.js`). By convention, `index.jsx` should render the `App` component.

```jsx
import React from "react";
import ReactDOM from "react-dom";
import App from "./Components/App";

ReactDOM.render(<App />, document.getElementById("root"));
```

### The app component

The app component will usually contain contain the basic app layout/scaffold.

```jsx
import React from "react";
import AppHeader from "./AppHeader";
import AppBody from "./AppBody";
import AppFooter from "./AppFooter";

class App extends React.Component {
  render() {
    return (
      <div>
        <AppHeader />
        <AppBody />
        <AppFooter />
      </div>
    );
  }
}

export default App;
```

Shorthand app component:

```jsx
import React from "react";
import AppHeader from "./AppHeader";
import AppBody from "./AppBody";
import AppFooter from "./AppFooter";

export default () => {
  return (
      <div>
        <AppHeader />
        <AppBody />
        <AppFooter />
      </div>
    );
});
```

### Functional components

Components are either functional or class based.

```jsx
import React from "react";

// Use either:
// const App = function () {
//   return <div>Hello there!</div>;
// };

// Or arrow function syntax:
const MyFunctionalComponent = () => {
  return <div>Hello there!</div>;
};

export default MyFunctionalComponent;
```

### Class components

State is only available in class components. Class components also support lifecycle methods.

```jsx
import React from "react";

class MyClassComponent extends React.Component {
  // Optional constructor:
  // constructor(props) {
  //   super(props);
  // }

  // Optional component lifecycle methods below:
  componentDidMount() {
    // Called when component is first rendered
  }

  componentDidUpdate() {
    // Called when component/state is updated
  }

  componentWillUnmount() {
    // Called when removing the component
  }

  // Component render method
  render() {
    return (
      <div>
        <p>Hello!</p>
      </div>
    );
  }
}

export default MyClassComponent;
```

## State

In React a `state` is a javascript object that contains data relevant to a particular component. State is only usable with class based components. The state is initialized when the component is created. Updating a state will result in a call to the components `render()` method. The only way to update a state is to use the function `setState()`.

```jsx
import React from "react";

class DemoStateComponent extends React.Component {
  // The only time state can be assigned is either here:
  state = { message: "Welcome" };

  // Or within the optional component constructor
  // constructor(props) {
  //   super(props);

  //   this.state = { message: "Welcome" };
  // }

  componentDidMount() {
    // The only way to modify the state is to call setState()
    this.setState({ "Welcome!!!" })
  }

  // Component render method
  render() {
    return (
      <div>
        <h3>message:</h3>
        <p>{this.state.message}</p>
      </div>
    );
  }
}

export default DemoStateComponent;
```

## Props

Parents can pass properties (props) to children. Props are read only values. The name given to the prop is used within the component to reference that value. Passing the value of `someString` to `ChildComponent`:

```jsx
import React from "react";
import ChildComponent from "./ChildComponent";

class App extends React.Component {
  state = { someString: "Hello!" };

  render() {
    return (
      <div>
        <ChildComponent thingToPass={this.state.someString} />
      </div>
    );
  }
}

export default App;
```

`ChildComponent` receives props from the parent component `thingToPass` in the code below contains the value of `someString` from the code above.

```jsx
import React from "react";

const ChildComponent = (props) => {
  return (
    <div>
      <p>{props.thingToPass}</p>
    </div>
  );
};

export default ChildComponent;
```

## Callback functions

Children can call functions passed by parents to send data up the hierarchy.

In the following code `App` is the parent of `DemoNameField`. The goal is to receive data from the child and display it in the parent.

```jsx
import React from "react";
import DemoNameField from "./DemoNameField";

class App extends React.Component {
  state = { name: "" };

  receiveName = (input) => {
    this.setState({ name: input });
  };

  render() {
    return (
      <div>
        <h1>Hello {this.state.name}</h1>
        <DemoNameField callback={this.receiveName} />
      </div>
    );
  }
}

export default App;
```

The `props` object sent to `DemoNameField` contains only a reference to `receiveName`. For clarity, it has been renamed to `callback` though renaming is optional.

```jsx
import React from "react";

class DemoNameField extends React.Component {
  state = { textInput: "" };

  onFormSubmit = (event) => {
    event.preventDefault();

    this.props.callback(this.state.textInput);
  };

  render() {
    return (
      <form onSubmit={this.onFormSubmit}>
        <label>Enter Name:</label>
        <input
          type="text"
          value={this.state.textInput}
          onChange={(event) => this.setState({ textInput: event.target.value })}
        ></input>
      </form>
    );
  }
}

export default DemoNameField;
```

The form instantly saves the text input to `DemoNameField`'s state. When the form is submitted, `DemoNameField` calls `onSubmit()`.

## Hooks

We can add class like functionality to functional components using React hooks.

### Use state

Initializing, modifying, and referencing state within a class component:

```jsx
// Initializing state
state = { myValue: 5, myString: "flowers" };
```

```jsx
// Modifying state
this.setState({ myValue: 11, myString: "apples" });
```

```jsx
// Referencing State
this.state.myValue;
this.state.myString;
```

Initializing, modifying, and referencing state within a functional component utilizing the `useState` hook:

```jsx
// to begin, import useState
import React, { useState } from "react";
```

```jsx
// Initializing state
const [myValue, setMyValue] = useState(5);
const [myString, setMyString] = useState("Flowers");
```

```jsx
// Modifying state
setMyValue(11);
setMyString("apples");
```

```jsx
// Referencing State
myValue;
myString;
```

Sample functional component with `useState` in action:

```jsx
import React, { useState } from "react";

export default function App() {
  const [count, setCount] = useState(0);

  const onButtonClick = () => {
    setCount(count + 1);
  };

  return (
    <div>
      <h1>Button clicks: {count}</h1>
      <button onClick={onButtonClick}>Click Me!</button>
    </div>
  );
}
```

### Use effect

Allows functional components to use methods similar to class lifecycle methods.

The `useEffect` hook takes in some code to execute as a parameter. The optional second parameter determines when this code should execute.

If the second parameter is an empty array, then the code will only be executed at the initial render:

```jsx
useEffect(() => {
  console.log("After initial render only");
}, []); // <-- Note the second parameter
```

If there is no second parameter, then the code will be executed at every render and at the initial render:

```jsx
useEffect(() => {
  console.log("After initial render and every render");
}); // <-- Note no second parameter
```

If the second parameter is an array containing a value (or values), then the code will only be executed when the data has been modified between renders and at the initial render:

```jsx
useEffect(() => {
  console.log("After initial render and every render with value modification");
}, [myMonitoredValue]); // <-- Note the second parameter
```

### Use ref

Allows functional components to access the DOM or other React components.
