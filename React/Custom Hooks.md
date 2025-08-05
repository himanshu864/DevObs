#react 

create custom hooks to export hooks and make code leaner just like functions.

> Every function that started with use in react is a custom hook

- We can create useState inside custom hooks, import them inside a component. Any states that belong to the custom hook, also belong to component.
- And upon resetting those states, the entire component with that custom hook gets re-rendered.

This code inside `App.jsx`
```jsx
function App() {
  // ...
  const [userPlaces, setUserPlaces] = useState([]);
  const [isFetching, setIsFetching] = useState(false);
  const [error, setError] = useState();
  //...
  useEffect(() => {
    async function fetchPlaces() {
      setIsFetching(true);
      try {
        const places = await fetchUserPlaces();
        setUserPlaces(places);
      } catch (error) {
        setError({ message: error.message || "Failed to fetch." });
      }
      setIsFetching(false);
    }

    fetchPlaces();
  }, []);
  // ...
}
```

Gets converted to
```jsx
function App() {
  // ...

const { isFetching, error, fetchedData } = useFetch(fetchUserPlaces, []);
  // ...
}
```

With `useFetch.jsx`
```jsx
import { useEffect, useState } from "react";

export function useFetch(fetchFn, initialValue) {
  const [isFetching, setIsFetching] = useState(false);
  const [error, setError] = useState();
  const [fetchedData, setFetchedData] = useState(initialValue);

  useEffect(() => {
    async function fetchPlaces() {
      setIsFetching(true);
      try {
        const places = await fetchFn();
        setFetchedData(places);
      } catch (error) {
        setError({ message: error.message || "Failed to fetch." });
      }

      setIsFetching(false);
    }

    fetchPlaces();
  }, [fetchFn]);

  return { isFetching, error, fetchedData };
}
```

Here we are able to update states from inside custom hooks and export value to the app component. But we can't update state from the component itself.

We can achieve that by export state updating function with state value from custom hooks.

- But you might think does updating state from one component affect another component's state that might be using the same custom hook?

The answer is No. Like components, custom Hooks gets recreated and are isolated to that specific component.

Might need to add this function as dependency when using useEffect.
