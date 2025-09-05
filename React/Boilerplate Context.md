#react 

### **App.jsx**
This is the root of the application. It wraps all components with the `ThemeProvider` to make the theme context available throughout the app.
```jsx
import ContextComponent from "./ContextComponent";
import ThemeProvider from "./ThemeProvider";

export default function App() {
  return (
    <ThemeProvider>
      <ContextComponent />
    </ThemeProvider>
  );
}
```

---

### **ThemeContext.jsx**
Defines a React context for the theme.
```jsx
import { createContext } from "react";

const ThemeContext = createContext();
export default ThemeContext;
```

---

### **ThemeProvider.jsx**
Manages the state for the theme and provides it to the application via `ThemeContext.Provider`.
```jsx
import { useState } from "react";
import ThemeContext from "./ThemeContext";

export default function ThemeProvider({ children }) {
  const [darkTheme, setDarkTheme] = useState(false);

  const toggleDarkTheme = () => {
    setDarkTheme((prev) => !prev);
  };

  return (
    <ThemeContext.Provider value={{ darkTheme, toggleDarkTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}
```

---

### **useTheme.js**
Custom hook to consume the theme context more cleanly.
```jsx
import { useContext } from "react";
import ThemeContext from "./ThemeContext";

export default function useTheme() {
  return useContext(ThemeContext);
}
```

---

### **ContextComponent.jsx**
Consumes the theme context using the `useTheme` hook and displays UI with theme toggling functionality.
```jsx
import useTheme from "./useTheme";

export default function ContextComponent() {
  const { darkTheme, toggleDarkTheme } = useTheme();

  return (
    <>
      <button onClick={toggleDarkTheme}>Toggle Theme</button>
      <div style={{ backgroundColor: darkTheme ? "grey" : "white" }}>
        Context Component
      </div>
    </>
  );
}
```
