# React-Cheet-Sheet
Basic syntax for reference

## Table of Contents

- [Introduction](#introduction)
- [JSX](#jsx)
- [Function Components](#function-components)
- [Class Components](#class-components)
- [Props](#props)
- [State](#state)

## Introduction
React is a declarative, efficient, and flexible JavaScript library for building user interfaces. It lets you compose complex UIs from small and isolated pieces of code called “components”.

```
class ShoppingList extends React.Component {
  render() {
    return (
      <div className="shopping-list">
        <h1>Shopping List for {this.props.name}</h1>
        <ul>
          <li>Instagram</li>
          <li>WhatsApp</li>
          <li>Oculus</li>
        </ul>
      </div>
    );
  }
}

// Example usage: <ShoppingList name="Mark" />
```

Here, ShoppingList is a React component class, or React component type. A component takes in parameters, called props (short for “properties”), and returns a hierarchy of views to display via the render method.

The render method returns a description of what you want to see on the screen. React takes the description and displays the result. In particular, render returns a React element, which is a lightweight description of what to render. Most React developers use a special syntax called “JSX” which makes these structures easier to write.

JSX comes with the full power of JavaScript. You can put any JavaScript expressions within braces inside JSX. Each React element is a JavaScript object that you can store in a variable or pass around in your program.

The ShoppingList component above only renders built-in DOM components like ```<div />``` and ```<li />```. But you can compose and render custom React components too. For example, we can now refer to the whole shopping list by writing ```<ShoppingList />```. Each React component is encapsulated and can operate independently; this allows you to build complex UIs from simple components.

## Why Immutability Is Important 
There are generally two approaches to changing data. The first approach is to mutate the data by directly changing the data’s values. The second approach is to replace the data with a new copy which has the desired changes.

### Data Change with Mutation 
```
var player = {score: 1, name: 'Jeff'};
player.score = 2;
// Now player is {score: 2, name: 'Jeff'}
```

### Data Change without Mutation
```
var player = {score: 1, name: 'Jeff'};

var newPlayer = Object.assign({}, player, {score: 2});
// Now player is unchanged, but newPlayer is {score: 2, name: 'Jeff'}

// Or if you are using object spread syntax proposal, you can write:
// var newPlayer = {...player, score: 2};
```

### Complex Features Become Simple 
Immutability makes complex features much easier to implement. An ability to undo and redo certain actions is a common requirement in applications. Avoiding direct data mutation lets us keep previous versions of the game’s history intact, and reuse them later.

### Detecting Changes 
Detecting changes in mutable objects is difficult because they are modified directly. This detection requires the mutable object to be compared to previous copies of itself and the entire object tree to be traversed.

Detecting changes in immutable objects is considerably easier. If the immutable object that is being referenced is different than the previous one, then the object has changed.

### Determining When to Re-Render in React 
The main benefit of immutability is that it helps you build pure components in React. Immutable data can easily determine if changes have been made which helps to determine when a component requires re-rendering.


### JSX
> React uses a syntax extension of JavaScript called JSX that allows you to write HTML directly within JavaScript. It lets you use the full programmatic power of JavaScript within HTML, and helps to keep your code readable. As JSX is a syntactic extension of JavaScript, you can actually write JavaScript directly within JSX.  To do this, you simply include the code you want to be treated as JavaScript within curly braces: { 'this is treated as JavaScript code' }

> JSX is not valid JavaScript, JSX code must be compiled into JavaScript. This function call ReactDOM.render(JSX, document.getElementById('root')). is what places your JSX into React's own lightweight representation of the DOM. React then uses snapshots of its own DOM to optimize updating only specific parts of the actual DOM.

```react
const JSX = (
  <div>
   {/* Comment */}
    <h1>This is a block of JSX</h1>
    <p>Here's a subtitle</p>
  </div>
);
```

> ReactDOM offers a simple method to render React elements to the DOM which looks like this: ReactDOM.render(componentToRender, targetNode), where the first argument is the React element or component that you want to render, and the second argument is the DOM node that you want to render the component to.
   ```react
    const JSX = (
        <div>
          <h1>Hello World</h1>
          <p>Lets render this to the DOM</p>
        </div>
      );
      
      // Must be called after the JSX element declarations, just like how you must declare variables before using them.
      ReactDOM.render(JSX, document.getElementById('challenge-node'))

      //  In JSX is that you can no longer use the word class to define HTML classes. This is because class is a reserved word in JavaScript. Instead, JSX uses className.
      // In fact, the naming convention for all HTML attributes and event references in JSX become camelCase. For example, a click event in JSX is onClick, instead of onclick

      const JSX = (
        <div className = "myDiv">
          <h1>Add a class to this div</h1>
        </div>
      );

      //  Any JSX element can be written with a self-closing tag, and every element must be closed. The line-break tag, for example, must always be written as <br /> in order to be valid JSX that can be transpiled.
      //  A <div>, on the other hand, can be written as <div /> or <div></div>. 
      const JSX = (
        <div>
          
          <h2>Welcome to React!</h2> <br />
          <p>Be sure to close all tags!</p>
          <hr />
              
        </div>
      );
```

## Function Components
In React, function components are a simpler way to write components that only contain a render method and don’t have their own state. Instead of defining a class which extends React.Component, we can write a function that takes props as input and returns what should be rendered. Function components are less tedious to write than classes, and many components can be expressed this way.

```react
function Square(props) {
  return (
    <button className="square" onClick={props.onClick}>
      {props.value}
    </button>
  );
}
```


## Class Components
> The other way to define a React component is with the ES6 class syntax. This creates an ES6 class Kitten which extends the React.Component class. So the Kitten class now has access to many useful React features, such as local state and lifecycle hooks.
 
> It uses super() to call the constructor of the parent class, in this case React.Component. The constructor is a special method used during the initialization of objects that are created with the class keyword. It is best practice to call a component's constructor with super, and pass props to both. This makes sure the component is initialized properly.
   ```react
      class Kitten extends React.Component {
        constructor(props) {
          super(props);
        }
      
        render() {
          return (
            <h1>Hi</h1>
          );
        }
      }

      // To compose these components together, you could create an App parent component which renders each of these three components as children. 
      // To render a component as a child in a React component, you include the component name written as a custom HTML tag in the JSX. 

      const ChildComponent = () => {
        return (
          <div>
            <p>I am the child</p>
          </div>
        );
      };
      
      class ParentComponent extends React.Component {
        constructor(props) {
          super(props);
        }
        render() {
          return (
            <div>
              <h1>I am the parent</h1>
              <ChildComponent />
            </div>
          );
        }
      };

      // React components are passed into ReactDOM.render() a little differently than JSX elements. 
     //  For JSX elements, you pass in the name of the element that you want to render. 
     // However, for React components, you need to use the same syntax as if you were rendering a nested component, for example ReactDOM.render(<ComponentToRender />, targetNode)

class TypesOfFood extends React.Component {
    constructor(props) {
      super(props);
    }
    render() {
      return (
        <div>
          <h1>Types of Food:</h1>
          <Fruits /> 
          <Vegetables /> 
        </div>
      );
    }
  };
  
  ReactDOM.render(<TypesOfFood />, document.getElementById('challenge-node'))
 ```

## Props
> In React, you can pass props, or properties, to child components. Say you have an App component which renders a child component called Welcome that is a stateless functional component. You can pass Welcome a user property by writing:
   ```react
  <App>
  <Welcome user='Mark' />
  </App>

const CurrentDate = (props) => {
    return (
      <div>
        <p>The current date is:  {props.date}</p>
      </div>
    );
  };
  
  class Calendar extends React.Component {
    constructor(props) {
      super(props);
    }
    render() {
      return (
        <div>
          <h3>What date is it?</h3>
          <CurrentDate />
        </div>
      );
    }
  };

  const CurrentDate = (props) => {
    return (
      <div>
        <p>The current date is:  {props.date}</p>
      </div>
    );
  };
  
  class Calendar extends React.Component {
    constructor(props) {
      super(props);
    }
    render() {
      return (
        <div>
          <h3>What date is it?</h3>
          <CurrentDate date={Date()} />
        </div>
      );
    }
  };

  // To pass an array to a JSX element, it must be treated as JavaScript and wrapped in curly braces.
  <ParentComponent>
  <ChildComponent colors={["green", "blue", "red"]} />
</ParentComponent>

const List= (props) => {
    return <p>{props.tasks.join(", ")}</p>
  };
  
  class ToDo extends React.Component {
    constructor(props) {
      super(props);
    }
    render() {
      return (
        <div>
          <h1>To Do Lists</h1>
          <h2>Today</h2>
          <List tasks={["Walk", "Cook", "Bake"]} />
          <h2>Tomorrow</h2>
          <List tasks={["Study", "Code", "Eat"]}/>
        </div>
      );
    }
  };

  // React also has an option to set default props. You can assign default props to a component as a property on the component itself and React assigns the default prop if necessary. 
  // This allows you to specify what a prop value should be if no value is explicitly provided. 
  // For example, if you declare MyComponent.defaultProps = { location: 'San Francisco' }, you have defined a location prop that's set to the string San Francisco, unless you specify otherwise. 
  // React assigns default props if props are undefined, but if you pass null as the value for a prop, it will remain null.

  const ShoppingCart = (props) => {
    return (
      <div>
        <h1>Shopping Cart Component</h1>
      </div>
    )
  };
  ShoppingCart.defaultProps = { items: 0}

  // React provides useful type-checking features to verify that components receive props of the correct type. 
  // For example, your application makes an API call to retrieve data that you expect to be in an array, which is then passed to a component as a prop. 
  // You can set propTypes on your component to require the data to be of type array. This will throw a useful warning when the data is of any other type.

  // The PropTypes.func part checks that handleClick is a function. Adding isRequired tells React that handleClick is a required property for that component.
  MyComponent.propTypes = { handleClick: PropTypes.func.isRequired }

  const Items = (props) => {
    return <h1>Current Quantity of Items in Cart: {props.quantity}</h1>
  };
  
  Items.propTypes = {
    quantity: PropTypes.number.isRequired
  };
  
  Items.defaultProps = {
    quantity: 0
  };
  
  class ShoppingCart extends React.Component {
    constructor(props) {
      super(props);
    }
    render() {
      return <Items />
    }
  };
  ```
     
 ## State
 > You create state in a React component by declaring a state property on the component class in its constructor. This initializes the component with state when it is created. The state property must be set to a JavaScript object. 
 
 > You have access to the state object throughout the life of your component. You can update it, render it in your UI, and pass it as props to child components. 
 
 > The state object can be as complex or as simple as you need it to be. Note that you must create a class component by extending React.Component in order to create state like this.

```react
class StatefulComponent extends React.Component {
  constructor(props) {
    super(props);
    // initialize state here
     this.state = {
      name : "Name"
    }
  }
  render() {
    return (
      <div>
        <h1>{this.state.name}</h1>
      </div>
    );
  }
};

class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name: 'freeCodeCamp'
    }
  }
  render() {
    const name = this.state.name;
    return (
      <div>
          <h1>{name}</h1>
      </div>
    );
  }
};

// React provides a method for updating component state called setState. You call the setState method within your component class like so: this.setState(), passing in an object with key-value pairs. 
// The keys are your state properties and the values are the updated state data. For instance, if we were storing a username in state and wanted to update it, it would look like this:

this.setState({
  username: 'Lewis'
});

class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name: 'Initial State'
    };
    this.handleClick = this.handleClick.bind(this);
  }
  handleClick() {
     this.setState({
      name: 'React Rocks!'
    });
  }
  render() {
    return (
      <div>
        <button onClick={this.handleClick}>Click Me</button>
        <h1>{this.state.name}</h1>
      </div>
    );
  }
};

// Counter
class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
      this.increment = this.increment.bind(this); 
      this.decrement = this.decrement.bind(this);
      this.reset = this.reset.bind(this);
  }
    increment(){this.setState({count: this.state.count + 1})}
    decrement(){this.setState({count: this.state.count - 1})}
    reset(){this.setState({count: 0})}
  render() {
    return (
      <div>
        <button className='inc' onClick={this.increment}>Increment!</button>
        <button className='dec' onClick={this.decrement}>Decrement!</button>
        <button className='reset' onClick={this.reset}>Reset</button>
        <h1>Current Count: {this.state.count}</h1>
      </div>
    );
  }
};

// Controlled Form
class MyForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: '',
      submit: ''
    };
    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }
  handleChange(event) {
    this.setState({
      input: event.target.value
    });
  }
  handleSubmit(event) {
    event.preventDefault();
  this.setState({
    input: '',
    submit: this.state.input
  });
  }
  render() {
    return (
      <div>
        <form onSubmit={this.handleSubmit}>
            <input value={this.state.input} onChange={this.handleChange}/>
          <button type='submit'>Submit!</button>
        </form>
           <h1>{this.state.submit}</h1>
      </div>
    );
  }
};
```
