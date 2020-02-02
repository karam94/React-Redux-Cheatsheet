# React-Redux-Cheatsheet
A React Redux cheatsheet. Made by myself, for myself, based on my own requirements &amp; how my head works. If it helps someone else, then awesome!

## Table of Contents
 - Functional Component
 - Class Component w/ Local State
 - Displaying/Rendering functions
 - OnClick Event
 - Conditionals
	 - If Rendering
	 - Ternary If Rendering
- Loops
	- Map a list of elements
- React Router
	- Routing
	- Routing with Parameters
- Lifecycle Methods
- Handling Forms
- HTTP Requests
- Snapshot Testing
- Redux
	- Types
	- Reducers
	- Actions

## Functional Component
Functional Components are best used in components that do not require a constructor/local state or the use of lifecycle methods.

### With Props
`<HelloWorld name="John" />`
	
	import React from  "react";
	import  "./style.scss";

	const HelloWorld = props => {
		return (
			<div className="danger">Hello {props.name}!</div>
		);
	};
	
	export default HelloWorld;

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
