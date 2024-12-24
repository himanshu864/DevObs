#react #dev 

# Memo
---
Wrap a component in `memo` to get a _memoized_ version of that component. This memoized version of your component will usually not be re-rendered when its parent component is re-rendered as long as its props have not changed. But React may still re-render it: memoization is a performance optimization, not a guarantee.

```jsx
import { memo } from 'react'

const SomeComponent = memo(function SomeComponent(props) {
	// ...
});
```

![[Pasted image 20240810135307.png]]
- We can also avoid memo() by cleverly structuring into different components, but that's case dependant. 

# useMemo
---
`useMemo` is a React Hook that lets you cache the result of a calculation between re-renders.

```jsx
const cachedValue = useMemo(calculateValue, dependencies)
```

Basically we can avoid re-running complex functions every time component renders while the parameters remain same.

## Virtual DOM
React uses virtual DOM to create new (to be inserted HTML) code from Tree components, and then compares what changed. And only updates that to keep performance light.

## Keys are important
Since instances of same components are isolated. One's state update change doesn't effect another's. But that's not exactly the case. When same components are used together. React updates them based on positioning. That's why when using for loop for displaying components, **Keys** are necessary. It uniquely identifies one component from another while avoiding any errors. Don't use index as keys since position is relative.

Use Million JS for even faster React
