#react 

React doesn’t automatically pass extra props/attributes to inner element. But we can manually forward them.

![[Pasted image 20241223161619.png]]

- **CoreConcepts.jsx** and **Examples.jsx** follow similar pattern with section then h2 and content

```jsx
export default function CoreConcepts() {
  return (
    <section id="core-concepts">
      <h2>Time to get started!</h2>
      <ul>
        {CORE_CONCEPTS.map((conceptItem) => (
          <Concept key={conceptItem.title} {...conceptItem} />
        ))}
      </ul>
    </section>
  );
}
```

- Which can be split up using `Section.jsx`
- And passing `id` or any other attribute by **forwarding prop** using `…props`

```jsx
export default function Section({ title, children, ...props }) { // merge
  return (
    <section {...props}> {/* Spreads attributes */}
      <h2>{title}</h2>
      {children}
    </section>
  );
}
```

- Concise `CoreConcept.jsx`
```jsx
export default function CoreConcepts() {
  return (
    <Section title="Time to get started!" id="core-concepts">
      <ul>
        {CORE_CONCEPTS.map((conceptItem) => (
          <Concept key={conceptItem.title} {...conceptItem} />
        ))}
      </ul>
    </Section>
  );
}
```

- Can also pass element name string via props and can set default value
