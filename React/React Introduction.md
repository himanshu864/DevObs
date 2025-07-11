#react 

## Define the goals, not the steps

### With React, you define the target UI state(s) - not the steps to get there!

- HTML inside javascript, weird stuff

# Setting up
---
- Create a Github repository and clone it
- Open in vscode and install react using Vite

```bash
$ npm create vite@latest
```

- Set a project-name
- Select framework (react) with language(javascript).
- cd to that project folder

```bash
npm install
```

- You can additionally add start script to **package.json** for `npm start` command

```json
"scripts": {
    "start" : "vite",
    "dev": "vite",
    // bla bla
  },
```

- Finally build the project using run dev or start

```bash
npm run dev || npm start
```

- By default port = 5173. Change using adding —port 3000 to package.json

```jsx
"scripts": {
  "dev": "vite --port 3000",
  "build": "vite build",
  "preview": "vite preview"
}
```

# Package.json

The `package.json` file is core to the NodeJs ecosystem and is a fundamental part of understanding and working with `Node.js`, `npm`, and even modern `JavaScript`. This file is used as a manifest, storing information about applications, modules, packages, and more.

- npm refers to package.json file of folder to install exact versions of packages to ensure the project works as intended.

## React doesn’t use javascript, instead transforms code for browsers to understand

- `React-script` dependency in package.json does that
- JSX is not a default Javascript feature, hence build process, using npm start
- Node Js also for converting react-script to concise JS for fast speed website