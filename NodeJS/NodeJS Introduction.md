#nodejs 

> Javascript runtime environment with chrome V8 engine and C++ embedded in it

Allows javascript to work at backend. Handle client-server, authentication, file handling and stuff

```bash
#Create a folder
npm init # -y for autocomplete
npm install express jsonwebtoken dotenv
npm install --global nodemon # install package globally
nodemon server.js # to watch and reload server on update
```

# Simple HTTP Server
---

```js
const { createServer } = require('node:http');

const hostname = '127.0.0.1';
const port = 3000;

const server = createServer((req, res) => {
    res.statusCode = 200;
    res.setHeader('Content-Type', 'text/html'); // display what? plain? html?
    res.end('<h1> Himanshu Aggarwal </h1>');
});

server.listen(port, hostname, () => {
    console.log(`Server running at <http://$>{hostname}:${port}/`);
});
```

- Node version manager (nvm) to manage and switch to different version of npm as per req.

# CommonJS Module
---
- uses `require` to import modules.
```js
const { createServer } = require('node:http');
```

- Loads the modules synchronously.
- We can console `__dirname`, `__filename` to get file directory and name in CommonJS

1. **Exporting Modules ( `math.js` )**
```js
function sum(a, b) {
    return a + b;
}
const diff = (a, b) => a - b;

module.exports = { sum, diff };
exports.mult = (a, b) => a * b;
```

2. **Import Modules ( `script.js` )**
```js
const { sum, diff, mult } = require("./math.js");

console.log(sum(3, 5));  // 8
console.log(diff(10, 4)); // 6
console.log(mult(4, 6));  // 24
```

3. **Package Configuration ( `package.json` )**
```json
{
  "type": "commonjs"
}
```

# EcmaScripts Modules
---
- **ES6** is modern and uses `import` to import modules
```jsx
import { createServer } from "http";
```

- Loads asynchronously
- We can import functions, variables using export (default) in ES6 modules

1. **Exporting Modules ( `math.js` )**
```js
export function sum(a, b) {
    return a + b;
}
export const diff = (a, b) => a - b;
export default (a, b) => a * b;
```

2. **Import Modules ( `script.js` )**
```js
import mult, { sum, diff } from "./math.mjs";

console.log(sum(3, 5));  // 8
console.log(diff(10, 4)); // 6
console.log(mult(4, 6));  // 24
```

3. **Package Configuration ( `package.json` )**
```json
{
  "type": "module"
}
```
