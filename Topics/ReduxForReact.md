# Redux for React<!-- omit in toc -->

Redux is an open source JavaScript library that helps manage state by centralizing state logic across the entire application.

## Table of contents<!-- omit in toc -->

- [Official website](#official-website)
- [Installation](#installation)
- [React state vs Redux](#react-state-vs-redux)
- [Terminology](#terminology)
  - [State](#state)
  - [Store](#store)
  - [Actions](#actions)
  - [Action creators](#action-creators)
  - [Reducers](#reducers)
  - [Dispatch](#dispatch)
- [Boilerplate](#boilerplate)

## Official website

For more information see: <https://redux.js.org>.

## Installation

to install the packages inside the project diretoru run:

```sh
npm install redux react-redux
```

## React state vs Redux

With React, you usually manage state within individual components and by passing around props or callbacks. Redux implements an app-wide centralized state with limited defined operations. The core of Redux is managing and updating `state` in a predictable fashion.

## Terminology

### State

In Redux, `state` is immutable. To update (or modify) the state you must copy and return a mutated copy of a previous state.

### Store

The current state resides in the Redux `store`. To read or update the store you define action(s) that implement specific operations.

### Actions

An `action` is a JavaScript object that has both a `type` and `payload` properties. A type is a simple text description of the operation being done to the payload (a state, or part of the state).

### Action creators

An `action creator` is a reusable function that returns an action object. They are used as convenience to avoid re-writing actions.

### Reducers

A `reducer` is a function that takes the current state and an action as parameters. A reducer will usually switch between all possible actions to select the appropriate operation, update the state if necessary, and return the state.

### Dispatch

The redux store receives actions via the `dispatch` method. The only way to update the store is to dispatch an action. The dispatch method takes an action parameter

## Boilerplate

After importing the redux packages, update the workspace structure to be similar to:

```text
my-app/
├─ node_modules/
├─ public/
│  ├─ index.html
├─ src/
│  ├─ actions/
│  │  ├─ index.js
│  ├─ components/
│  │  ├─ MyComponent.jsx
│  ├─ reducers/
│  │  ├─ index.js
│  ├─ index.jsx
├─ .gitignore
├─ package.json
├─ README.md
```

Redux boilerplate (`index.jsx`):

```jsx
import React from "react";
import ReactDOM from "react-dom";
import { Provider } from "react-redux";
import { createStore } from "redux";

import App from "./components/App";
import reducers from "./reducers";

ReactDOM.render(
  <Provider store={createStore(reducers)}>
    <App />
  </Provider>,
  document.getElementById("root")
);
```

Action boilerplate (`actions/index.js`):

```jsx
export const actionA = () => {
  return { type: "ACTION_A_NAME" };
};

export const actionB = () => {
  return { type: "ACTION_B_NAME", payload: null };
};
```

Reducer boilerplate (`reducers/index.js`):

```jsx
import { combineReducers } from "redux";

export default combineReducers({
  reducerPlaceholder: () => "placeholder",
});
```

Connecting Redux to components boilerplate:

```jsx
import React from "react";
import { connect } from "react-redux";
import { actionA, actionB } from "../actions";

class MyComponent extends React.Component {
  render() {
    return <div>Content</div>;
  }
}

const mapStateToProps = (state) => {
  return { someProp: state.someValue };
};

export default connect(mapStateToProps, { actionA, actionB })(MyComponent);
```
