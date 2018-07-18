## Proptypes

https://reactjs.org/docs/typechecking-with-proptypes.html

## State
https://reactjs.org/docs/state-and-lifecycle.html

## Binding Patterns
https://medium.freecodecamp.org/react-binding-patterns-5-approaches-for-handling-this-92c651b5af56


### Constructor Binding

```javascript
constructor(props) {
  super(props);
  this.handleChange = this.handleChange.bind(this);
}
```

## Techniques

### React: Pass State as Props to Child Components

```javascript
class MyApp extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name: 'CamperBot'
    }
  }
  render() {
    return (
       <div>
         <Navbar name={this.state.name} />
       </div>
    );
  }
};

class Navbar extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
    <div>
      <h1>Hello, my name is: {this.props.name}</h1>
    </div>
    );
  }
};
```


### React: Pass a Callback as Props

```javascript
class MyApp extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      inputValue: ''
    }
    this.handleChange = this.handleChange.bind(this);
  }
  handleChange(event) {
    this.setState({
      inputValue: event.target.value
    });
  }
  render() {
    return (
       <div>
        <GetInput input={this.state.inputValue} handleChange={this.handleChange}/>
        <RenderInput input={this.state.inputValue}/>
        
       </div>
    );
  }
};

class GetInput extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h3>Get Input:</h3>
        <input
          value={this.props.input}
          onChange={this.props.handleChange}/>
      </div>
    );
  }
};

class RenderInput extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h3>Input Render:</h3>
        <p>{this.props.input}</p>
      </div>
    );
  }
};
```

## React Lifecycle Methods

Here are the main lifecycle methods:

### componentWillMount(): called before the render method

```javascript
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
  }
  componentWillMount() {
    // change code below this line
    console.log("Mounting component");
    // change code above this line
  }
  render() {
    return <div />
  }
};
```

### componentDidMount():
- This method is called after a component is mounted to the DOM
- Here is where we put API calls/any calls to server, since it also updates the state if we call the this.setState() method
- This is the best place to attach event listeners

```javascript
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      activeUsers: null
    };
  }
  componentDidMount() {
    setTimeout( () => {
      this.setState({
        activeUsers: 1273
      });
    }, 2500);
  }
  render() {
    return (
      <div>
        <h1>Active Users: { this.state.activeUsers }</h1>
      </div>
    );
  }
};
``` 

### componentWillReceiveProps() 
This is called whenever a component is receiving new props. This method receives the new props as an argument, which is usually written as nextProps. You can use this argument and compare with this.props and perform actions before the component updates. For example, you may call setState() locally before the update is processed.

*Note: Example below with componentDidUpdate()*

### componentDidUpdate()
This is called immediately after a component re-renders. Note that rendering and mounting are considered different things in the component lifecycle.

```javascript
class Dialog extends React.Component {
  constructor(props) {
    super(props);
  }
  componentWillUpdate() {
    console.log('Component is about to update...');
  }
  // change code below this line
  componentWillReceiveProps(nextProps){
    console.log(this.props);
    console.log(nextProps);    
  }

  componentDidUpdate(){
    console.log('Dialog updated');
  }
  // change code above this line
  render() {
    return <h1>{this.props.message}</h1>
  }
};

class Controller extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      message: 'First Message'
    };
    this.changeMessage = this.changeMessage.bind(this);
  }
  changeMessage() {
    this.setState({
      message: 'Second Message'
    });
  }
  render() {
    return (
      <div>
        <button onClick={this.changeMessage}>Update</button>
        <Dialog message={this.state.message}/>
      </div>
    );
  }
};
```

### shouldComponentUpdate()
But React provides a lifecycle method you can call when child components receive new state or props, and declare specifically if the components should update or not. This method is a useful way to optimize performance. For example, the default behavior is that your component re-renders when it receives new props, even if the props haven't changed. You can use shouldComponentUpdate() to prevent this by comparing the props. The method must return a boolean value that tells React whether or not to update the component

```javascript
shouldComponentUpdate(nextProps, nextState) {
  console.log('Should I update?');
  // Only updates the DOM if the value is even
  return nextProps.value % 2 === 0 ;
}
```
### componentWillUpdate()

### componentWillUnmount()
- This is called before a component is destroyed
```javascript
componentDidMount() {
  document.addEventListener('keydown', this.handleKeyPress)
}
// Here we will do the cleanups 
componentWillUnmount() {
  document.removeEventListener('keydown', this.handleKeyPress);
}
// change code above this line
handleEnter() {
  this.setState({
    message: this.state.message + 'You pressed the enter key! '
  });
}
handleKeyPress(event) {
  if (event.keyCode === 13) {
    this.handleEnter();
  }
}
```

