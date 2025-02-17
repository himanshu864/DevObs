#react  

# Form Submission
---

- *for*'s in labels are replaced by htmlFor in react.
- By Default, whenever a button in clicked inside a form, a HTTP request is send to server and the page reloads.
![[Pasted image 20240826144748.png]]
To remedy that:
- change default button type from submit to *button*.
OR
- can add onSubmit function to form instead of onClick function to button. And add `event.preventDefault()` to the start of handler Function. This cancels event is possible.

Then we can further **send** collected **data** **to** a standalone **API** instead of react server.

### We can access forms data in react using:
---
### 1. **States**: Two way binding
- Lot of code
- Easy resetting

```jsx
export default function Login() {
  // define state as object to handle multiple inputs
  const [inputs, setInputs] = useState({ email: "", password: "" });

  function handleSubmit(event) {
    event.preventDefault();
    console.log(inputs);
  }

  // return immediate object. {object} inside ().
  // to access and change any value in obj, use []
  function handleInputChange(identifier, value) {
    setInputs((prevStates) => ({ ...prevStates, [identifier]: value }));
  }

  return (
    <form onSubmit={handleSubmit}>
	  <label htmlFor="email">Email</label>
	  <input
		id="email"
		type="email"
		name="email"
		onChange={(event) => handleInputChange("email", event.target.value)}
		value={inputs.email}
	  />
	  {/*...*/}
    </form>
  );
}
```

### 2. Ref:
Simple connect to email and password and console.
But resetting input fields can be hard using refs. It's not recommended.
Also will be increasingly difficult as input fields increase.

### 3. FormData
- Native Browser API.
- `FormData` simplifies collecting form data, especially when handling multiple checkboxes or inputs.
- Converting `FormData` to an object with `Object.fromEntries(fd.entries())` makes it easy to work with the data in your JavaScript code.

```jsx
  function handleSubmit(event) {
    event.preventDefault();

	// get input data with name fields
    const fd = new FormData(event.target);
    const data = Object.fromEntries(fd.entries());
    
    // for multiple checkboxes with same name. use .getAll()
    const acquisitionChannel = fd.getAll("acquisition");
    
    data.acquisition = acquisitionChannel;
    console.log(data);
  }
```

- Also add a quick little reset code to reset the form
```javascript
function handleSubmit(event) {
    // ... reset inputs
    event.target.reset();
}
```

# Input Validation
---
Add custom functions and states to check if input was editing, is blurred, and is valid and stuff.

Basically you want to error only when input is done being edited and remove when focused again. Easy Stuff.

