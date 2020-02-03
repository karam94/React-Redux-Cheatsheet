

# React-Redux-Cheatsheet
A React Redux cheatsheet. Made by myself, for myself, based on my own requirements &amp; how my head works. If it helps someone else, then awesome! Pull requests with improvements are more than welcome.

## Table of Contents
 - [Functional Components](#Functional-Components)
 - [Class Components with Local State](#Class-Components-with-Local-State)
 - [Children Components](#Children-Components)
 - [Rendering functions](#Rendering-Functions)
 - OnClick Event
- Handling Forms/OnSubmit Event
- Conditionals: If Rendering
- Conditionals: Ternary If Rendering
- Loops: Map a list of elements
- React Router: Routing
- React Router: Routing with Parameters
- Lifecycle Methods
- HTTP Requests
- Enzyme/Snapshot Testing
- Redux: Overview
- Redux: Types
- Redux: Reducers
- Redux: Actions
- React Hooks

## Functional Components
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

## Class Components with Local State
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
## Children Components
```jsx
<HelloWorld name="John">
  Greetings
</HelloWorld>
```
```jsx
import React from  "react";
import  "./style.scss";

// Prints: "Greetings John!"
const HelloWorld = ({ children }) => {
  return (
    <div className="danger">{children} {props.name}!</div>
  );
};
	
export default HelloWorld;
```
## Rendering Functions
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
Loops through `cartItems`...
Note: If you are unfamiliar with where `cartItems` is coming from or the `mapPropsToState()` function, assume `cartItems` is just a list for now and ignore `react-redux`-related boilerplate.
```jsx
import React from  "react";
import { connect } from  "react-redux";
import CheckoutItem from  "../../components/checkout-item/checkout-item.component";
import  "./checkout.styles.scss";

const CheckoutPage = ({ cartItems }) => {
  return (
    <div className="checkout-page">
      {cartItems.map(cartItem  => (
        <CheckoutItem key={cartItem.id} cartItem={cartItem}  />
      ))}
    </div>
  );
};

const mapStateToProps =  state  => ({
  cartItems: state.cart.cartItems
});

export default connect(mapStateToProps)(CheckoutPage);
```

## React Router: Routing 
If a Route has `exact` then it will only match the exact specified path. If it does not use `exact` then React Router will try and match the closest possible route and still try to navigate the user.

The below in App.js sets up the routes, so that we can `<Link />` to them in components.
```
npm install react-router-dom 
```
```jsx
import { Switch, Route, Redirect } from  "react-router-dom";

class App extends React.Component {
  render() {
    return (
      <div>
        <Switch>
          <Route exact path="/" component={HomePage}  />
          <Route path="/shop" component={ShopPage}  />
          <Route 
            exact path="/signin" 
            render={() =>
              this.props.currentUser ? (
                <Redirect to="/" />
              ) : (
                <SignInAndSignUpPage />
              )
            }
          />
        </Switch>
       </div>
    );
  }
}
```
```jsx
import { Link } from  "react-router-dom";

<div className="options">
  <Link className="option" to="/shop">SHOP</Link>
  <Link className="option" to="/contact">CONTACT</Link>
</div>
```

## React Router: Routing with Parameters
```jsx
import { Switch, Route } from  "react-router-dom";
import ShopComponent from "./shopComponent";

<div>
  <Switch>
    <Route path="/shop/:shopId" component={ShopComponent}>SHOP</Link>
    <Route path="/contact">CONTACT</Link>
  </Switch>
</div>
```
```jsx
import React from  "react";

const ShopComponent = ({ match }) => {
  return (
    <div>Your shop id is: {match.params.shopId}!</div>
  );
};
	
export default ShopComponent;
```

## Lifecycle Methods
|Method|Explanation  |
|--|--|
| render() | Renders your component. Occurs during the mounting & updating of a component. |
| componentDidMount() | Called as soon as a component is mounted and ready. Good place to initiate initial API calls to populate a component's data from.|
| componentDidUpdate() | Called whenever a component is updated. Good place to react to prop or state changes. |
| componentWillUnmount() | Called just before a component is unmounted and destroyed. |
| shouldComponentUpdate() | Used to provide a bool function, who's output determines whether to update a component or not. |
| getDerivedStateFromProps() | Called just before render(), right after props are updated. |
| getSnapshotBeforeUpdate() | Called just before a component is updated. The value returned is passed on to componentDidUpdate(). |

## HTTP Requests
`npm install axios`

### GET
```js
axios.get('/user', {
params: {id: 1}
}).then(function (response) {
   //some logic here
})
.catch(function (error) {
   //some logic here
})
.finally(function () {
   //some logic here
});
```

### POST
```js
axios.post('/user', {
    firstName: 'Bob',
    id: 2
}).then(function (response) {
    //some logic here
})
.catch(function (error) {
    //some logic here
});
```

### Async/Await
```js
getUsers = async () => {
  let res = await axios.get("/user?id=1");
  let { data } = res.data;
  this.setState({ users: data });
};
```

## Enzyme/Snapshot Testing
```js
// setupTests.js
import { configure } from  "enzyme";
import Adapter from  "enzyme-adapter-react-16";

configure({ adapter:  new  Adapter() });
```
```js
import { shallow, mount } from  "enzyme";
import React from  "react";
import CustomButton from  "/custom-button.component";

it("expect to render CustomButton component", () => {
  expect(shallow(<CustomButton  />).length).toEqual(1);
});

it("expect to render CustomButton component snapshot", () => {
  expect(shallow(<CustomButton  />)).toMatchSnapshot();
});

it("expect to render Google CustomButton component snapshot", () => {
  const wrapper =  mount(<CustomButton  isGoogleSignIn  />);
  expect(wrapper.find(".custom-button").hasClass("google-sign-in")).toEqual(true);
});
```
