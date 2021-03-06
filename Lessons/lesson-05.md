# FEW 2.3 - Lesson 5

## Conditional Rendering

Conditional rendering is the process of showing one component or another depending on data or possibly showing or not showing a component at all. 

## Learning Objectives

1. Identify use cases for conditional rendering
1. Define patterns used for conditional rendering
1. Use conditional rendering

## Conditional Rendering

Commonly in React, you will need to render different components under different conditions. Here are two patterns you can apply to your work: 

**Pattern 1**

The idea is to render one component or another depending on some logic. One method to handle this is with a function:

```JS 
function WeatherData(isLoaded) {
  if (isLoaded) {
    return <Weather />
  }

  return <Loading />
}
```

Here is a function that returns either the Weather component or the Loading Component. 

```JS
function App() {
  return (
    <div>
      {WeatherData(false)} // displays <Loading />
    </div>
  )
}
```

You can take the idea above one step further. Since a Component is a function you treat it like a component. **Note! parameters are passed via props!**

```JS 
function WeatherData({ isLoaded }) { // Notice the change here!
  if (isLoaded) {
    return <Weather />
  }

  return <Loading />
}
```

Here is a function that returns either the Weather component or the Loading Component. 

```JS
function App() {
  return (
    <div>
      {<WeatherData isLoaded={true} />} // displays <Weather />
    </div>
  )
}
```

**Pattern 2** - Assign a JSX element to variables and render that. This works for situations where a list of components might be used. 

```JavaScript
function WhatToEat(props) {
  const { time } = props
  let element
  if (time === 'morning') {
    element = <Eggs />
  } else if (time === 'lunch') {
    element = <Burrito />
  } else {
    element = <Icecream />
  }

  return (
    <div>
      {element}
    </div>
  )
}
```

**Pattern 3** Use the && operator. Here you'd render a component or render nothing. 

```JS 
<div>
  <h1>Hello!</h1>
  {unreadMessages.length > 0 &&
    <h2>
      You have {unreadMessages.length} unread messages.
    </h2>
  }
</div>
```

Here `false && 99` evaluates to false, and `true && 99` evaluates to 99. 

**Pattern 4** The ternary operator is like a single line if else. 

```JSX
function LoginButton(props) {
  const { isLoggedIn } = props;
  return (
    <div>
      {isLoggedIn
        ? <LogoutButton />
        : <LoginButton />
      }
    </div>
  );
}
```

The ternary operator `condition ? truthy expression : falsey expression` works with three elements: a condition, a truthy expression, and a falsey experssion. 

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator

**Pattern 5** In some cases you'll want to show a component or nothing at all. React won't render `null` if it appears in a component. 

```JSX 
function Warning({ show, message }) {
  if (show === false) {
    return null
  }
  return (
    <div>
      Warnging: {message}
    </div>
  ) 
}

function App() {
  return (
    <div>
      <Warning show={false}> // displays nothing
      <Warning show={true} message="Look out!"> // displays the message
    </div>
  )
}
```

### Lifecycle methods 

A lifecycle method is a method that is called when a component is created, updated, or will be removed. Use lifecycle methods to: 

- Initialize components 
- Apply updates
- Clean up resources

Two important lifecycel methods are: 

- `componentDidMount()` - Called when a component is created and added to the DOM. This is good place to start your component and initialize it's activities.
- `componentWillUnmount()` - Is called when a component is about to be removed from the DOM. Use this to clean up resources a component will not lobnger need. 

```JS
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  componentDidMount() {
  }

  componentWillUnmount() {
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```

### Using Conditional Rendering

This might be good when you want to see the logic at the point where something is rendered. 

Read more about [Conditional Rendering in React](https://reactjs.org/docs/conditional-rendering.html)

Conditional Rendering techniques

- A function returns a component
- Element Variables
- Inline if with logical && Operator
- Inline if-else with Conditional Operator (ternary)
- Prevent Component from rendering

https://scotch.io/tutorials/7-ways-to-implement-conditional-rendering-in-react-applications

## In Class 

Start on Assignment 3. In this assignment you will create an app that works with a web API. It will need to load data and display it. To build the app you will make use of conditional rendering.

[Assignment 3](../Assignments/Assignment-03)

## After Class

After class your goal is to use the ideas from this class make your portfolio web site a "multipage" navigable site with React Router. 

[Assignment 3](../Assignments/Assignment-03)

## Additional Resources

1. https://reactjs.org/docs/conditional-rendering.html
1. https://reactjs.org/docs/thinking-in-react.html
1. https://reactjs.org/docs/design-principles.html

