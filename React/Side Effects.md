#react

---
> Side effects are tasks that are required for app to work correctly, but don't directly impact current component render cycle.

- If a necessary function causes react to re-render again and again. Will cause an infinity loop.
- Which is a side-effect. If we want a function to only render once. We can use useEffect with an empty array. Or a trigger if it changes throughout runtime

You probably don't need useEffect, if you aren't trying to synchronize with some external system.

# Effect Dependencies
---
- useEffect takes in a second parameter. An array with a list of dependencies. Whenever any dependency changes. useEffect function runs and component re-renders.

This is console every time a component re-renders
```jsx
useEffect(() => {
	console.log("render")
})
```

This hook also takes a second parameter, Array. Whenever something inside that array changes, useEffect is called
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

You should add dependencies if you're using props or state functions inside useEffect.

# Cleaning up Effect
---
*You can return a function inside useEffect which can help clean up component after it is unmounted or right before useEffect re-executes*

In this case, we want model to automatically conform after 3 seconds of opening. And we want Timeout to clear after we close model or unmount component.

```jsx
  useEffect(() => {
    console.log("TIMER STARTED");
    const timer = setTimeout(() => {
      onConfirm();
    }, 3000);

    return () => {
      console.log("TIMER CLEARED");
      clearTimeout(timer);
    };
  }, []);
```

Also be sure to only display dialog when open. Otherwise useEffect will run in background, since dialog is always open just not visible.

Now it works perfectly!

#### Problem with Object and Function Dependencies
---
When you pass object/function as dependency to an useEffect() there is a possibility for an infinite loop.

- useEffect - DeleteConfirmation.jsx
```jsx
useEffect(() => {
	const timer = setTimeout(() => onConfirm(), 3000);
	return () => clearTimeout(timer);
}, [onConfirm]);
```

- function - App.jsx
```jsx
function handleRemovePlace() {
	// ...
}
```

Suppose you pass a function to useEffect and it re-executes, which causes entire component to re-render and which re-creates the function. In this case, even through the function is the exact same, javascript does not compare them as same. Which will cause useEffect to trigger and re-execute. And the whole process repeat infinitely.

And that's where useCallback comes in

# useCallback
---
`useCallback` is a React Hook that lets you cache a function definition between re-renders.

Basically this stops functions to re-create whenever component re-renders, to stop useEffect with that as dependency to re-execute.

Talk about the 3 R's, am I right?

```jsx
const handleRemovePlace = useCallback(function handleRemovePlace() {
	// ...
}, []);
```

Just wrap the function and pass in all **reactive** values referenced (state, prop, function, object, etc) inside an array as second parameter as dependencies.

