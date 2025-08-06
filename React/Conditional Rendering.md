#react 

Your components will often need to display different things depending on different conditions. In React, you can conditionally render JSX using JavaScript syntax like `if` statements, `&&`, and `? :` operators.

- If define initial State as *falsy*, eg: useState`()`, `(””)`, `(null)`, `(0)` or `(false)`. And use that as a condition to render content.

```jsx
{selectedTopic ? (
  <div id="tab-content">
    <h3>{EXAMPLES[selectedTopic].title}</h3>
  </div>
) : (
  <p>Please select a topic</p>
)}
```

```jsx
{!selectedTopic && <p>Please select a topic</p>}

{selectedTopic && (
  <div id="tab-content">
    <h3>{EXAMPLES[selectedTopic].title}</h3>
  </div>
)}
```

> Must have a parent element wrapping both JSX expression

```jsx
let tabContent = <p>Please select a topic</p>;

if (selectedTopic) {
  tabContent = (
    <div id="tab-content">
      <h3>{EXAMPLES[selectedTopic].title}</h3>
      <p>{EXAMPLES[selectedTopic].description}</p>
      <pre>
        <code>{EXAMPLES[selectedTopic].code}</code>
      </pre>
    </div>
  );
}
```

- Define variable using if condition outside JSX
- And simply use output in-place

```jsx
{tabContent}
```
