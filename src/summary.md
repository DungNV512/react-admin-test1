# ReactJs Summary

## Components and Props

React has a few different kinds of components:
..* Default React component subclass
..* The old style createClass component
..* The Stateless Function component
..* The Presentational component
A component is like a JS function, take in parameters, calls `__props__`, and returns a hierarchy of views via the `_render_` method.
...The `_render_` method returns a __React Element__(see more JSX or `React.createElement('div')`).
__All React components must act like pure functions with respect to their props.__

### Controlled components

### Why Immutability Is Important
... Replace the data with a copy of obj 
..* Increase component & overall app performance
..* Easier Undo/Redo
..* Tracking changes
..* Determining when to re-render: Learn more about `shouldComponentUpdate()` and _how to build pure component_' [here](https://facebook.github.io/react/docs/optimizing-performance.html#examples)

### Functional components

... Replace component that only consist of a `render` method = function that take props and returns what should be render.

## State

State is similar to props, but private and fully controlled by component. Local state is a feature available only to classes.

### Mounting / Unmounting in React and lifecycle hooks

### Using state correctly

..* Do not modify State directly
..* State updates may be Asynchronous
... Use an arrow function to update the counter into state. That function will receive the previous state as the first argument, the props at the time the update is applied as the second argument
..._Wrong_: `this.setState({counter: this.state.counter + this.props.increment,});`
..._Correct_:`this.setState((prevState, props) => ({counter: prevState.counter + props.increment}));`
..* State updates are merged

### Top-down data flow

## JSX

JSX is a syntax extension to JS, produces React "elements".
After complication, JSX extension become JS objects, mean that can use it inside of `if` statements, `for` loops, assign it to variables, accept it as arguments, return it from function.
..* Attributes use quotes `""` for string or curly braces `{}` for JS expression
..* JSX prevent XSS attack
..* JSX Represents Objects

## Handling events
..* React events are named using camelCase, not lowercase
..* With JSX you pass a function as the event handler, rather than a string.
..* Cannot return `false`, must call `preventDefault`.
..* Not need to call `addEventListener`. Instead, just provide a listener when the element is initially rendered.
..* Bind this???
... Two ways instead
...1 Property initializer syntax `handleClick = () => {}`. Recommend using this syntax.
...2 Arrow function in the callback `onClick={(e) => this.handleClick(e)}`. With this syntax, a different callback is created each time React Component renders. If this callback is passed as a props to lower components, they might do an extra re-rendering => performance problem.

## Conditional Rendering
..* Inline If with Logical && Operator
... `true && expression` always evaluates to `expression` - `false && expression` always evaluates to `false`
..* Inline If-Else with Conditional Operator
... `condition ? true : false`
..* Preventing component from rendering
... To hide component, return `null` instead of its render output. This do not affect the firing of the component's lifecycle method, `componentWillUpdate` will still be called.

## Lists and keys

### Lists

Usually, lists are renderd inside a component, using `map()` to loop through array 

### Keys

Key is a special attribute that need to include when creating list of elements, help React identify which items have changed/added/removed.
The best way to pick a key is to use a string.

## Forms
..* `<input>` Tag
..* `<textarea>` Tag
..* `<select>` Tag

# Redux
## Core principles
..* Single source of truth
..* State is read-only
..* Changes are made with pure functions
## Redux component 
..* Reducers are functions that take two arguments, previous state and an action; return next state as an entirely new object
..* A Redux Provider `{provider}` allows to connect React to Redux store.
..* The react-redux package will, essentially, give us a way to pull Redux's state into React as props via `{connect}`.
..* The redux-promise is a library that allows to add a middleware function to store. If it receives a promise as a payload from an action, it will dispatch the resolved value of that promise. Middleware functions are basically a layer added between a request and a response that perform some sort of check or transformation on data. 
...This solve issue: all Redux actions are synchronous by default => no result to pass reducer.
..* The `react-router-redux`package
### Actions
..* The action itself: a plain JavaScript object, two pieces: a type (required) and a payload (only required if want to pass data along with action)
..* The action type. In Redux, this is almost always expressed as a const in all caps so that it can be exported for use in other parts of our application (such as our reducers). You can just use regular strings, but it makes it that much more likely that you'll introduce bugs via typos or if your action names change.
..* The action creator: can import these into containers and pass them into child components via props