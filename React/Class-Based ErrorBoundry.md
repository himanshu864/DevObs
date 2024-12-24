#react

![[Pasted image 20240817161418.png]]

- render method is used to return all renderable code. wow
- Extent class to Component and use *this* property to access props.
- Hooks like useState, useEffect weren't a thing in react til v.16 or something
- So need to define and update state using constructor method
- Also here state needs to be an object
- Components also support setState built-in which *merges* new states with prev, instead of overriding it.
- use *this.state* to access your states and call state updating via function via that weird javascript this usage. `this.handleUpdate.bind(this)`

```jsx
import {Component} from 'react';

// Import and wrap this content around components that could crash
class ErrorBoundary extends Component {
	// Create State
	constructor() {
		super();
		this.state = { hasError : false };
	}
	// Update State
	toggleUsersHandler(error) {
		console.log(error);
		this.setState({hasError : true});
	}
	// Return JSX
	render() {
		if(this.state.hasError)
			return <p>Something Went Wrong!</p>;
		
		return this.props.children;
	}
}
```

![[Pasted image 20240817164023.png]]
Bro just leave the company that still uses this shit.

