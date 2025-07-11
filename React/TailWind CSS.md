#react 

### Installation inside [[Boilerplate For MERN Project]]

Defined kind-of intuitive names. Follow documentation.

- For media queries:

```jsx
<header className="flex flex-col items-center mt-8 mb-8 md:mb-16">
```

For medium screen .i.e. greater than 768px min width margin-bottom 4rem. Else 2rem

```jsx
hover:bg-amber-500
// for hover pseudo class
```

- Dynamically styling with tailwind

```jsx
export default function Input({ label, invalid, ...props }) {
  let labelClasses = "block mb-2 text-xs font-bold tracking-wide uppercase";
  let inputClasses = "w-full px-3 py-2 leading-tight border rounded shadow";

  // be sure to add extra whitespace in front before styling dynamically
  if (invalid) {
    labelClasses += " text-stone-400";
    inputClasses += " text-red-500 bg-red-100 border-red-300";
  } else {
    labelClasses += " text-stone-300";
    inputClasses += " text-gray-700 bg-stone-300";
  }

  return (
    <p>
      <label className={labelClasses}>{label}</label>
      <input className={inputClasses} {...props} />
    </p>
  );
}
```
