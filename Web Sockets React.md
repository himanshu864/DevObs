[Reference](https://socket.io/how-to/use-with-react)
*Date Created*: 2025-03-17
*Date Modified*: 2025-03-17

---
## Basic Setup

1. Create a server repository and install `socket.io` library.
2. `server.js`
```js
const io = require("socket.io")(3000, {
  cors: {
    origin: "http://localhost:5173",
  },
});

io.on("connection", (socket) => {
  console.log("User connected!", socket.id);

  // Listen and Emit custom events
  socket.on("foo", (msg) => {
    io.emit("bar", `${msg} from ${socket.id}`);
  });

  socket.on("disconnect", () => {
    console.log("User disconnected!", socket.id);
  });
});
```

3. Create a React repository and install `socket.io-client` library.
4. Add `socket.js` inside `/src` folder.
```js
import { io } from "socket.io-client";

const URL = "http://localhost:3000";

// By default, connects automatically on load
export const socket = io(URL, {
  autoConnect: false,
});
```

5. Use `useEffect` to connect and use sockets in `App.jsx`
```jsx
import { useEffect, useState } from "react";
import { socket } from "./socket";
import { ConnectionManager } from "./components/ConnectionManager";

export default function App() {
  const [isConnected, setIsConnected] = useState(socket.connected);
  const [messages, setMessages] = useState([]);

  // Handle states with socket connection
  useEffect(() => {
    socket.on("connect", () => {
      setIsConnected(true);
      socket.emit("foo", "Hello Everyone!"); // emit a custom event
    });

    socket.on("disconnect", () => setIsConnected(false));

    // Listen for a custom event
    socket.on("bar", (msg) => {
      setMessages((prev) => [...prev, msg]);
    });

    // clean up event listens on unmount
    return () => {
      socket.off("connect");
      socket.off("disconnect");
      socket.off("bar");
    };
  }, []);

  return (
    <>
      {/* Socket Dynamic Rendering */}
      <p>Connected: {isConnected ? "Yes" : "No"}</p>
      <h2>Messages</h2>
      <ul>
        {messages.map((msg, i) => (
          <li key={i}>{msg}</li>
        ))}
      </ul>
      <ConnectionManager />
    </>
  );
}
```

6. `ConnectionManager.jsx` component to demonstration connection handling inside a component.
```jsx
import { socket } from "../socket";

export function ConnectionManager() {
  return (
    <>
      <button onClick={() => socket.connect()}>Connect</button>
      <button onClick={() => socket.disconnect()}>Disconnect</button>
    </>
  );
}
```

---

**Connection and Disconnection in React**

```jsx
useEffect(() => {
  // no-op if the socket is already connected
  socket.connect();

  return () => {
    socket.disconnect();
  };
}, []);
```

> [!Tip]
> 1. Clean up very important to prevent duplicate events and reconnection on each render.
> 2. Also carefully emit events from client in React with StrictMode to prevent duplicates.

**Loading and emit after timeout in React**

```jsx
  function onSubmit(event) {
    event.preventDefault();
    setIsLoading(true);

    socket.timeout(5000).emit('create-something', value, () => {
      setIsLoading(false);
    });
  }
```
