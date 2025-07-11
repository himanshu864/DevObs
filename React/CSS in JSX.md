#react 

## Inline styling in React:

- Inside **2 curly braces**

1. { .. } evaluates to an expression in JSX.
2. { key: value } implies a javascript object.

```jsx
<p style={{ color: "red" }}>artists</p>
```

## Dynamic Inline styling

```jsx
style={{ backgroundColor: emailNotValid ? "#fed2d2" : "#d1d5db" }}
```

- Use Ternary operator when applying styles dynamically, since falsy isn’t a value

```jsx
className={emailNotValid ? "invalid" : undefined}
```

### Apply some classes dynamically

```jsx
<label className={`label ${emailNotValid ? "invalid" : ""}`}>
```