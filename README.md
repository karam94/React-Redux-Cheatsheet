
# React-Redux-Cheatsheet
A React Redux cheatsheet. Made by myself, for myself, based on my own requirements &amp; how my head works. If it helps someone else, then awesome!

## Table of Contents
 - Functional Component
 - Class Component w/ Local State
 - Displaying/Rendering functions
 - OnClick Event
- Handling Forms/OnSubmit Event
- Conditionals: If Rendering
- Conditionals: Ternary If Rendering
- Loops: Map a list of elements
- React Router
	- Routing
	- Routing with Parameters
- Lifecycle Methods
- HTTP Requests
- Snapshot Testing
- Redux
	- Types
	- Reducers
	- Actions

## Functional Component
Functional Components are best used in components that do not require a constructor/local state or the use of lifecycle methods.

### With Props
```jsx
<HelloWorld name="John" />
```
```jsx
import React from  "react";
import  "./style.scss";

const HelloWorld = props => {
  return (
    <div className="danger">Hello {props.name}!</div>
  );
};
	
export default HelloWorld;
```

## Class Component w/ Local State
Class Components are best used in components that require a constructor/local state or the use of lifecycle methods.

### With Props
```jsx
<HelloWorld name="John" />
```

```jsx
import React from  "react";
import  "./style.scss";
	
class HelloWorld extends React.Component {
  constructor(props){
    super(props);

    this.state = {
      city: "",
      age: 10			
    }
  }

  render() {
    const { name } = this.props; // Allows {name} instead of {props.name} below.

    return (
      <div className="danger">Hello {name}!</div>
    );
  }
}
	
export default HelloWorld;
```

## Displaying/Rendering Functions
```jsx
const HelloWorld = props => {
  return (
    <div className="danger">Hello {getUsername()}!</div>
  );
};

function getUsername() {
  return "John";
}
```

```jsx
const HelloWorld = props => {
  return (
    {printWelcomeMessage()}
  );
};

function printWelcomeMessage() {
  return (
    <div className="danger">Hello John!</div>
  );
}
```

## OnClick Event
```jsx
const HelloWorld = props => {
  return (
    <div className="danger">
      Hello <a href="#" onClick={this.showWelcomeAlert}>John!</a>
    </div>
  );
};

showWelcomeAlert = (e) => {
  e.preventDefault();
  console.log('Welcome!');
}
```

## Handling Forms/OnSubmit Event
```jsx
import React from  "react";
import  "./style.scss";

class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: ''
    };
  }

  handleChange = event => {
    const { value } = event.target;
    this.setState({value: value});
  }

  handleSubmit = event  => {
    event.preventDefault();
    alert('A name was submitted: ' + this.state.value);
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}

export default NameForm;
```

## Conditionals: If Rendering
```jsx
render() {
  return (
    {DisplayMessage()}
  );
}

function DisplayMessage() {
  const { show } = this.state;
  
  if(show){
    return (
      <div>Hello World</div>
    );
  } else {
      return (
      <div>Goodbye World</div>
    );
  }
}
```

## Conditionals: Ternary If Rendering
```jsx
render() {
  return (
    {this.state.show ? <div>Hello World</div> : <div>Goodbye World</div>}
  );
}
```

## Loops: Map a list of elements
Loops through `cartItems`..
```jsx
import React from  "react";
import { connect } from  "react-redux";
import CheckoutItem from  "../../components/checkout-item/checkout-item.component";
import  "./checkout.styles.scss";

const CheckoutPage = ({ cartItems }) => {
  return (
    <div className="checkout-page">
      {cartItems.map(cartItem  => (
        <CheckoutItem key={cartItem.id}  cartItem={cartItem}  />
      ))}
    </div>
  );
};

const mapStateToProps =  state  => ({
  cartItems: state.cart.cartItems
});

export default connect(mapStateToProps)(CheckoutPage);
```
