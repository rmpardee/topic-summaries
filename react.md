# Component
A collection of JS functions that produce HTML
- synonymous with 'View' 
- they are composed, reused, and nested
- can communicate with each other

**JSX**: HTML written into your JS
- To write JS inside your JSX, put it inside curly brackets

Note: Whenever you're writing JSX, you need to import React at the top of your file with
```js
import React from 'react';
```
as Babel will convert JSX into `React.createElement(...)`

## Functional Components
Don't contain state (are stateless)
- essentially just the render method of class components

**Example functional component**:
```js
const App = () => (
  <div>Hello World</div>
);
```
(note parentheses instead of curly brackets after fat arrow is the ES6 way of saying everything in the parentheses is what is returned by the function)

### Props
- `props` is an argument passed in from the parent when a component is created
- `props` is immutable; it cannot change because a functional component is only created once and not re-rendered

```js
const ToDoList = (props) => (
  <ul>
    <li>{ props.todos[0] }</li>
    <li>{ props.todos[1] }</li>
    <li>{ props.todos[2] }</li>
  </ul>
);

const App = () => (
  <div>
    <ToDoList todos={['Mix', 'Bake', 'Cool']} />
  </div>
);
```

### Rendering to the DOM
To actually render to the DOM, you need a _separate_ library, ReactDOM.
```js
import ReactDOM from 'react-dom';
```

When invoking `ReactDOM.render`, it takes two parameters:
1. an instance of a component (by writing as a JSX element it will be an instance, such as `<App />`),
2. where to render it on the DOM
```js
ReactDOM.render(<App />, document.querySelector('.container'));
```



## Class Components
- stores data that cannot be passed in `props` with `state`
  - `state` is an ordinary JS object used to record and react to events
- whenever the `state` object changes, the render method is re-run
- class components must have a `constructor` method and a `render` method

```js
class SearchBar extends React.Component {
  constructor(props) {
    // required to call the parent method with super
    super(props)

    // initialize state object here. It's the only place you would have this.state = to something
    // (only place this.state is defined, any other place where it's changed you should be using this.setState)
    this.state = { term: '' };
  }

  // props not passed into render function (like with functional components)
  // but instead accessed with `this.props`
  render() {
    return (
      <input
        // note the value is only set when the component re-renders
        // (the state change is what's driving the re-assignment of value)
        value = { this.state.term }
        onChange = { event => this.setState({ term: event.target.value })}
      />
    );
  }
}
```

### Exporting
Make sure to export any components you want to nest inside other components

```js
export default SearchBar;
```
