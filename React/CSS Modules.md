#react 

By default, CSS is scoped globally even when you split and import it in JSX. But you can scope it to a component using your Build Process( Vite in our case).

- **Header.module.css**
```css
.paragraph {
    text-align: center;
    color: #a39191;
    margin: 0;
}
```

- Header.jsx
```jsx
import logo from "../assets/logo.png";
import classes from "./Header.module.css";

export default function Header() {
  return (
      <p className={classes.paragraph} style={{ color: "crimson" }}>
        A community of artists and art-lovers.
      </p>
  );
}
```

This applies .paragraph is only scoped to Header component’ p, as build process modifies it.
