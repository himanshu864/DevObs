#react 

`npm install styled-components`

```jsx
import { styled } from "styled-components";

const ControlContainer = styled.div`
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
`;

export default function AuthInputs() {
	return (
		<ControlContainer>
			// content
		</ControlContainer>
	)
}
```

Use this to replace div and it’s styles inside index.css to a single styled component.div element.

- They also use children prop, to wrap them around content
- They also forward all passed props to underlying JSX

## Dynamic and Conditional Styling

```jsx
<ControlLabel className={`label ${emailNotValid ? "invalid" : ""}`}>

// css
label.invalid {
color: #f87171;
}
```

Above styling can be done using Styled Components. So we’ll use that.

```cpp
const ControlLabel = styled.label`
  // ...
  // color: ${(props) => (props.invalid ? "#f87171" : "#6b7280")};
  color: ${({ invalid }) => (invalid ? "#f87171" : "#6b7280")};

// 1. Pass invalid
export default function AuthInputs() {
	return <ControlLabel invalid={emailNotValid}>Email</ControlLabel>
}
```

- Use template literals, where you can pass conditions inside a function, which takes props as input. Might destructure
- You don’t want to collide with in-built props. that’s why common convention to use $invalid.

## Nested Rules, Media Queries and Pseudo Selectors

To apply styling to elements in inside a styled component. Simple place all css inside double backticks. And change all instances of component’s element to `&` .

- No need to create separate styled components for every element

```cpp
const StyledHeader = styled.header`
  display: flex;
  margin-bottom: 2rem;

	// applies to img inside header  
  & img {
    object-fit: contain;
  }

  p {
    text-align: center;
  }

	// apply pseudo selectors using this.
	// Applies hover to children if whitespace in b/w
	&:hover {
    background-color: #f0920e;
  }
  
  @media (min-width: 768px) {
  
    margin-bottom: 4rem; // applies to header
    
    & h1 {
      font-size: 2.25rem;
    }
  }
`;
```

- Modularize components that might be used multiple times

- Export a single component which multiple commonly used styled components together. Like label and input. And export them as a function

- Eg: this→ **authInputs.jsx**

```jsx
import { styled } from "styled-components";

const ControlLabel = styled.label`
  display: block;
  color: ${({ $invalid }) => ($invalid ? "#f87171" : "#6b7280")};
`;

const ControlInput = styled.input`
  width: 100%;
  border-color: ${({ $invalid }) => ($invalid ? "#f73f3f" : undefined)};
`;

export default function AuthInput() {
// ...
return (
		<p>
		  <ControlLabel $invalid={emailNoValid}>Email</ControlLabel>
		  <ControlInput
		    type="email"
		    $invalid={emailNoValid}
		    onChange={(event) =>
		      handleInputChange("email", event.target.value)
		    }
		  />
		</p>
		<p>
		  <ControlLabel $invalid={passwordNotValid}>Password</ControlLabel>
		  <ControlInput
		    type="password"
		    $invalid={passwordNotValid}
		    onChange={(event) =>
		      handleInputChange("password", event.target.value)
		    }
		  />
		</p>
  );
}
```

- Can be converted into ⇒
- **CustomInput.jsx**

```jsx
import { styled } from "styled-components";

const ControlLabel = styled.label`
  display: block;
  color: ${({ $invalid }) => ($invalid ? "#f87171" : "#6b7280")};
`;

const ControlInput = styled.input`
  width: 100%;
  border-color: ${({ $invalid }) => ($invalid ? "#f73f3f" : undefined)};
`;

const CustomInput = ({ label, invalid, ...props }) => {
  return (
    <p>
      <ControlLabel $invalid={invalid}> {label} </ControlLabel>
      <ControlInput $invalid={invalid} {...props} />
    </p>
  );
};
export default CustomInput;
```

- **authInputs.jsx**

```jsx
import CustomInput from "./CustomInput.jsx";

export default function AuthInputs() {
// ...
  return (
      <CustomInput
        label="Email"
        invalid={emailNotValid}
        type="email"
        onChange={(event) => handleInputChange("email", event.target.value)}
      />
      <CustomInput
        label="Password"
        invalid={passwordNotValid}
        type="password"
        onChange={(event) => handleInputChange("password", event.target.value)
        }
      />
  );
}
```

- Now we have a nice reusable Label-Input component with variable Label Name, invalid state and Custom props on input. Which imports two styled components, concisely.

Summary:

- Think and code CSS like react
- Scoped to a component
- But can be annoying to have CSS in same file and modularize every like component