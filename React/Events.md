#react 

Instead of targeting an element, and then adding event listener to it. In React, we can simply use `onClick={function}` to add events **declaratively**. (WHAT, instead of HOW)

- The advantage of defining these event handler function inside the component function is that they have access to the component’s props and state.
- But that function can’t be accessed outside component function

```jsx
export default function TabButton(props) {
  function handleClick() {
    console.log("meow");
  }
  return <button onClick={handleClick}>{props.children}</button>;
}
```

---

1. `children` is the only prop with defined name, should be first. We can custom make any other prop as we like.
2. Since handleClick function doesn’t have access to anything outside JSX file, it can't change content dynamically.
3. That’s why we need to forward a pointer from outside JSX to act as a callback trigger.

- `App.jsx`
```jsx
function handleSelect() {
	console.log("Meow Meow");
}

return (
	<TabButton onSelect={handleSelect}>Component</TabButton>
);
```

- `TabButton.jsx`
```jsx
export default function TabButton({ children, onSelect }) {
  return <button onClick={onSelect}>{children}</button>;
}
```

Here, the `handleSelect` function is passed from `App.jsx` to `TabButton.jsx` as a prop (`onSelect`). When the button inside `TabButton` is clicked, it triggers the `handleSelect` function defined in the parent component.

1. Since we want to dynamically change value, we want to identify which button was clicked by configuring it.
2. But we can’t directly pass a string, otherwise it would be executed
3. That’s why we pass an anonymous function with handler(target) inside of it, which only passes when clicked

```jsx
function handleSelect(tab) {
    if (tab == 1) {
      console.log("Components");
    }
}
return <TabButton onSelect={() => handleSelect(1)}>Component</TabButton>;
```
