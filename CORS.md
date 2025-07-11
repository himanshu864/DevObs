#nodejs #react 

Cross-Origin Resource Sharing basically doesn't responds to server that belong to different origin i.e. (domain, port, etc).

OR

**Cross-Origin Resource Sharing** ([CORS](https://developer.mozilla.org/en-US/docs/Glossary/CORS)) is an [HTTP](https://developer.mozilla.org/en-US/docs/Glossary/HTTP)-header based mechanism that allows a server to indicate any [origins](https://developer.mozilla.org/en-US/docs/Glossary/Origin) (domain, scheme, or port) other than its own from which a browser should permit loading resources.

This doesn't allow strangers to access private data. So it's good.

You just need to setup a ***PROXY*** in your backend to whitelist any address.
- Also try enabling cors first. Then google how to do that in your tech stack.


# Connect Frontend and Backend
---

- Can install cors library in NodeJS to allow Access Control from different Origins
- use useEffect in React and *Axios* package to get data from API's
- add Proxy in vite.config.js to avoid CORS error
```javascript
export default defineConfig({
  server: {
    proxy: {
      // string shorthand: http://localhost:5173/foo -> http://localhost:4567/foo
      '/foo': 'http://localhost:4567',
      // with options: http://localhost:5173/api/bar-> http://jsonplaceholder.typicode.com/bar
      '/api': {
        target: 'http://jsonplaceholder.typicode.com',
        changeOrigin: true,
        rewrite: (path) => path.replace(/^\/api/, ''),
      },
      // with RegExp: http://localhost:5173/fallback/ -> http://jsonplaceholder.typicode.com/
      '^/fallback/.*': {
        target: 'http://jsonplaceholder.typicode.com',
        changeOrigin: true,
        rewrite: (path) => path.replace(/^\/fallback/, ''),
      },
      // Using the proxy instance
      '/api': {
        target: 'http://jsonplaceholder.typicode.com',
        changeOrigin: true,
        configure: (proxy, options) => {
          // proxy will be an instance of 'http-proxy'
        },
      },
      // Proxying websockets or socket.io: ws://localhost:5173/socket.io -> ws://localhost:5174/socket.io
      // Exercise caution using `rewriteWsOrigin` as it can leave the proxying open to CSRF attacks.
      '/socket.io': {
        target: 'ws://localhost:5174',
        ws: true,
        rewriteWsOrigin: true,
      },
    },
  },
})
```

Learn when actually connect a backend and frontend together. And deploy of course.

Maybe today.