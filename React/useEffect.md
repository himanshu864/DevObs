#react 

Re-renders component whenever **effect dependencies** changes.

This is console every a component re-renders

```jsx
useEffect(() => {
	console.log("render")
})
```

This hook also takes a *second parameter, Array.* Whenever something inside that array changes, useEffect is called

- Very useful for fetching data from backend.

```jsx
useEffect(() ⇒ {
	console.log("only once!")
}, []) // an empty array never changes, so only runs once
```

To set some state to initial, whenever trigger changes

```jsx
useEffect(() => {
  setState(0);
}, [trigger]);
```
