---
tags:
  - "#javascript"
references:
  - https://youtu.be/JUORwadOU7s?si=n0LbO8WgGQdkrGZR
date_created: 2025-03-31
date_modified: 2025-04-01
---
---
# Installation

### 1. Verify Node.js Installation

You already installed Node.js from the official website. Let's check if it's properly installed:

```sh
node -v
npm -v
```

This should return version numbers. If not, try reinstalling Node.js.

### 2. Install TypeScript & `ts-node`

Since you installed TypeScript via Homebrew, it's system-wide. But projects should have their own local dependencies. Install TypeScript and `ts-node` locally:

```sh
npm install --save-dev typescript ts-node @types/node
```

To check if it's installed:

```sh
npx ts-node --version
```

### 3. Initialize TypeScript Configuration (`tsconfig.json`)

Run:

```sh
npx tsc --init
```

This generates a `tsconfig.json` file. Modify it for a clean setup:

```json
{
  "compilerOptions": {
    "target": "ESNext",
    "module": "CommonJS",
    "outDir": "./dist",
    "rootDir": "./src",
    "strict": true,
    "esModuleInterop": true
  },
  "include": ["src"],
  "exclude": ["node_modules"]
}
```

### 4. Project File Structure

A good structure for a TypeScript project:

```
my-ts-project/
│── src/
│   ├── index.ts
│── dist/  (Generated JS files)
│── node_modules/
│── package.json
│── tsconfig.json
│── .gitignore
```

Run:

```sh
mkdir src
touch src/index.ts
echo "console.log('Hello TypeScript!');" > src/index.ts
```

### 5. Running TypeScript Code

Use `ts-node` to run TypeScript directly:

```sh
npx ts-node src/index.ts
```

To compile and run via Node:

```sh
npx tsc
node dist/index.js
```

### 6. Adding Scripts for Convenience

Modify `package.json`:

```json
"scripts": {
  "dev": "ts-node src/index.ts",
  "build": "tsc",
  "start": "node dist/index.js"
}
```

Now, you can run:

```sh
npm run dev   # Run TypeScript directly
npm run build # Compile to JavaScript
npm start     # Run compiled JS
```

### 7. (Optional) Installing `nodemon` for Auto-Restart

For auto-reloading:

```sh
npm install --save-dev nodemon
```

Modify `package.json`:

```json
"scripts": {
  "dev": "nodemon --ext ts --exec ts-node src/index.ts"
}
```

Run:

```sh
npm run dev
```

Now, changes in `.ts` files auto-restart the app.

---
# Code

### 1. **Simple Function Conversion**

**JavaScript:**

```javascript
function add(a, b) {
  return a + b;
}
```

**TypeScript:**

```typescript
function add(a: number, b: number): number {
  return a + b;
}
```

_Explanation:_  
In the TypeScript version, each parameter (`a` and `b`) is explicitly typed as a `number`, and the return type is also declared as `number`.

### 2. **Using Interfaces for Object Shapes**

**JavaScript:**

```javascript
const person = {
  name: "John",
  age: 30
};
```

**TypeScript:**

```typescript
interface Person {
  name: string;
  age: number;
}

const person: Person = {
  name: "John",
  age: 30
};
```

_Explanation:_  
An `interface` named `Person` is defined to describe the shape of the object. The variable `person` is then annotated with the `Person` interface.

### 3. **Function with Object Parameter**

**JavaScript:**

```javascript
function greet(person) {
  console.log("Hello " + person.name);
}
```

**TypeScript:**

```typescript
interface Person {
  name: string;
  age?: number; // Optional property
}

function greet(person: Person): void {
  console.log("Hello " + person.name);
}
```

_Explanation:_  
The function parameter is typed using the `Person` interface. Here, `age` is marked as optional with the `?`, and the function return type is declared as `void` since it doesn't return a value.

### 4. **Converting a Class**

**JavaScript:**

```javascript
class Animal {
  constructor(name) {
    this.name = name;
  }
  speak() {
    console.log(this.name + " makes a noise.");
  }
}
```

**TypeScript:**

```typescript
class Animal {
  name: string;
  
  constructor(name: string) {
    this.name = name;
  }
  
  speak(): void {
    console.log(this.name + " makes a noise.");
  }
}
```

_Explanation:_  
TypeScript requires that class properties like `name` are declared with a type. The constructor and methods also include type annotations for their parameters and return types.

### 5. **Arrow Function Conversion**

**JavaScript:**

```javascript
const multiply = (a, b) => a * b;
```

**TypeScript:**

```typescript
const multiply = (a: number, b: number): number => a * b;
```

_Explanation:_  
The arrow function parameters are annotated as numbers and the return type is declared, ensuring type safety.

---

By adding these type annotations and interfaces, you gain better code clarity, improved error checking during compilation, and enhanced IDE support. These examples illustrate common patterns you can apply to gradually convert and improve your JavaScript projects with TypeScript.
