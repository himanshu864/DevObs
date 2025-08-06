#react 

- Every useState has it's own scope which makes sure the entire web page doesn't re-execute but only the component, when state is changed
### Component Instances work in Isolation

- One's state is completely independent of another.

# Updating State Based on old State

![[Pasted image 20241223162058.png]]

- React schedules state updates in future. Not instantly
- Pass a function to immediately change current state

**Example**: When directly changed state

```jsx
const [isEditing, setIsEditing] = useState(false);

function handleEditing() {
	setIsEditing(!isEditing); // false to true
	setIsEditing(!isEditing); // false to true
}
```

When passed a function

```jsx
const [isEditing, setIsEditing] = useState(false);

function handleEditing() {
	setIsEditing((isEditing) => !isEditing); // false to true
	setIsEditing((isEditing) => !isEditing); // true to false
}
```

- Also pass a function as Initial State to useState if state is heavy, to avoid rerunning useState every time re-render, and not slow down website
- useState works a little differently when passed an object. setState overrides prev entirely

```jsx
function App() {
	const [state, setState] = useState({count : 4, theme: 'blue'})
	const count = state.count
	const theme = state.theme

	function decrementCount() {
		setState(prevState => {
			return {...prevState, count: prevState.count - 1}
		})
	}
}
```

## Two way Binding

```jsx
// to dynamically change playerName when input change
const [playerName, setPlayerName] = useState(initialName);

function handleInput(event) {
    setPlayerName(event.target.value);
}

<input type="text" value={playerName} onChange={handleInput} required />
```

When same element listens to change, and feeds value back into it.

- Create deep copy when State depends on array or Object. Since passed by reference. Hence should change in an immutable way.

# Lifting State up

When multiple components need to share a variable or state. Define that state in the Lowest Common Ancestor. And then keep passing down the state

![[Pasted image 20241223163409.png]]
