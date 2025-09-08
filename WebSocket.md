#nodejs 

Our usual client-server architecture works on request and response. Client requests to server. And server responds. And connection ends there~

But what if, server has a message of client? Then it's gonna have to wait until client requests again. Which is not ideal.

One thing we can do is to request sever every second to check of responses. Which is called **Polling**. And that is far more ideal. Too much burden on server. Overkill.

Another solution is **Web socket**.

- Computer communication protocol providing full-duplex communication.
- They basically update normal HTTP connection to Web Socket connection.
- For Persistent connection and Real time communication.

---
## Socket.io
Socket.IO is composed of two parts:

- A server that integrates with (or mounts on) the Node.JS HTTP Server (the [`socket.io`](https://www.npmjs.com/package/socket.io) package)
- A client library that loads on the browser side (the [`socket.io-client`](https://www.npmjs.com/package/socket.io-client) package)

```javascript
// app.js
const express = require("express");
const { createServer } = require("node:http");
const { Server } = require("socket.io");

const app = express();
const server = createServer(app);
const io = new Server(server);

app.get("/", (req, res) => {
  res.sendFile(__dirname + "/public/index.html");
});

io.on("connection", (socket) => {
  console.log("a user connected");

  socket.on("disconnect", () => {
    console.log("user disconnected!");
  });
});

server.listen(3000);
```

- Need to create server using Node, and then upgrade using **Socket.io**.
- Initialize `io` (input/output) instance by passing server (HTTP) object
- *Need to **sendFile** and not EJS for web sockets*

```html
<!--/public/index.html-->
<body>
  <ul id="messages"></ul>
  <form id="form" action="">
    <input id="input" autocomplete="off" /><button>Send</button>
  </form>

  <script src="/socket.io/socket.io.js"></script>
  <script>
    const socket = io();
  </script>
</body>
```

That’s all it takes to load the `socket.io-client`, which exposes an `io` global (and the endpoint `GET /socket.io/socket.io.js`), and then connect.

- Each socket fires a special `connection` and  `disconnect` event.
- Open different tabs and check console.

---
## Emit
The main idea behind Socket.IO is that you can send and receive any events you want, with any data you want

- Take input from user
```javascript
// index.html
const socket = io();

const form = document.getElementById('form');
const input = document.getElementById('input');

form.addEventListener("submit", (e) => {
  e.preventDefault();
  if (input.value) {
	socket.emit("chat message", input.value)
	input.value = '';
  }
})
```

- and console it
```javascript
// app.js
io.on("connection", (socket) => {
  console.log("a user connected");

  socket.on("chat message", (msg) => {
    console.log("user msg: ", msg);
  });
});
```
Taadaa!! Now we can access messages from user, no probeleemo

emit() to **send a message to all the connected clients**. This code will notify when a user connects to the server. socket.

Here,
- We first **emit** chat message from client to server using `socket.emit()`
- Then we console message on server using `socket.on()` inside `io.on()`

---
Now, we need to emit event from server to rest of the users

- **app.js**
```javascript
io.on("connection", (socket) => {
  socket.on("chat message", (msg) => {
    io.emit("chat message", msg);
  });
});
```
For that simply use `io.emit()` on server to broadcast message to everyone including sender.

- **index.html**
```javascript
const socket = io();

const form = document.getElementById('form');
const input = document.getElementById('input');
const messages = document.getElementById('messages');

form.addEventListener("submit", (e) => {
  e.preventDefault();
  if (input.value) {
	socket.emit("chat message", input.value)
	input.value = '';
  }
})

socket.on('chat message', (msg) => {
  const item = document.createElement('li');
  item.textContent = msg;
  messages.appendChild(item);
  window.scrollTo(0, document.body.scrollHeight);
});
```

Here first the client is sending message from this browser to the server. Which is then broadcasted to all the users on the socket. And then that message is received and displayed on browser.

And with that, we have a working real-time chat application!

---

We can send anything and everything inside **socket.emit()**. Whether it be client to server or vice-versa
### Basic Emit
Client to
```javascript
socket.emit('hello', 'world', 'also');
```
Server
```javascript
io.on('connection', (socket) => {
  socket.on('hello', (arg1, arg2) => {
    console.log(arg1); // 'world'
    console.log(arg2); // 'also'
  });
});
```
##### OR
Server to
```javascript
io.on('connection', (socket) => {
  socket.emit('hello', {1, 'x'});
});
```
Client
```javascript
socket.on('hello', (arg) => {
  console.log(arg); // {1, 'x'}
});
```

- We can also send callback/promises
- Can create arbitrary channel for sockets to join and leave. called **rooms**

## Cheat sheet

```javascript
socket.emit('message', "this is a test"); //sending to sender-client only

socket.broadcast.emit('message', "this is a test"); //sending to all clients except sender

socket.broadcast.to('game').emit('message', 'nice game'); //sending to all clients in 'game' room(channel) except sender

socket.to('game').emit('message', 'enjoy the game'); //sending to sender client, only if they are in 'game' room(channel)

socket.broadcast.to(socketid).emit('message', 'for your eyes only'); //sending to individual socketid

io.emit('message', "this is a test"); //sending to all clients, include sender

io.in('game').emit('message', 'cool game'); //sending to all clients in 'game' room(channel), include sender

io.of('myNamespace').emit('message', 'gg'); //sending to all clients in namespace 'myNamespace', include sender

socket.emit(); //send to all connected clients

socket.broadcast.emit(); //send to all connected clients except the one that sent the message

socket.on(); //event listener, can be called on client to execute on server

io.sockets.socket(); //for emiting to specific clients

io.sockets.emit(); //send to all connected clients (same as socket.emit)

io.sockets.on() ; //initial connection from a client.
```

---
## Good to know

- **One Server, One Memory Space:** All clients connect to one server (NodeJS) instance, which holds the user data in its memory.
- **Socket IDs as Unique Identifiers:** Socket.io automatically generates and manages these IDs for tracking connected clients. Both client and server have access to their own socket IDs.

## Optional Approach to simple chatting application

##### `index.html` (public)

```html
<!DOCTYPE html>
<html>
  <head>
    <meta name="viewport" content="width=device-width,initial-scale=1.0" />
    <title>Socket.IO Chat</title>
    <style>
      body {
        margin: 0;
        padding-bottom: 3rem;
        font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
          Helvetica, Arial, sans-serif;
      }

      #form {
        background: rgba(0, 0, 0, 0.15);
        padding: 0.25rem;
        position: fixed;
        bottom: 0;
        left: 0;
        right: 0;
        display: flex;
        height: 3rem;
        box-sizing: border-box;
        backdrop-filter: blur(10px);
      }

      #input {
        border: none;
        padding: 0 1rem;
        flex-grow: 1;
        border-radius: 2rem;
        margin: 0.25rem;
      }

      #input:focus {
        outline: none;
      }

      #form > button {
        background: #333;
        border: none;
        padding: 0 1rem;
        margin: 0.25rem;
        border-radius: 3px;
        outline: none;
        color: #fff;
      }

      #messages {
        list-style-type: none;
        margin: 0;
        padding: 0;
      }

      #messages > li {
        padding: 0.5rem 1rem;
      }

      #messages > li:nth-child(odd) {
        background: #efefef;
      }
    </style>
  </head>

  <body>
    <ul id="messages"></ul>
    <form id="form" action="">
      <input id="input" autocomplete="off" /><button>Send</button>
    </form>

    <script src="/socket.io/socket.io.js"></script>
    <script src="script.js"></script>
  </body>
</html>
```

##### `script.js` (client)

```javascript
const socket = io();

const form = document.getElementById("form");
const input = document.getElementById("input");
const messages = document.getElementById("messages");

const appendMessage = (text) => {
  const item = document.createElement("li");
  item.textContent = text;
  messages.appendChild(item);
  window.scrollTo(0, document.body.scrollHeight);
};

// when client joins
const userName = prompt("WusYaName");
socket.emit("new user", userName);

// when client sends a message
form.addEventListener("submit", (e) => {
  e.preventDefault();
  if (!input.value) return;
  socket.emit("new message", socket.id, input.value);
  input.value = "";
  input.focus();
});

// whenever someone joins
socket.on("user connected", (socketId, name) => {
  if (socketId == socket.id) appendMessage("You connected");
  else appendMessage(`${name} connected`);
});

// when someone messages
socket.on("chat message", (socketId, name, msg) => {
  if (socketId == socket.id) appendMessage(`You: ${msg}`);
  else appendMessage(`${name}: ${msg}`);
});

// when someone disconnects
socket.on("user disconnect", (socketId, name) => {
  if (socketId == socket.id) appendMessage("You disconnected");
  else appendMessage(`${name} disconnected`);
});
```

##### `server.js` (server)

```javascript
const express = require("express");
const { createServer } = require("node:http");
const { Server } = require("socket.io");

const app = express();
const server = createServer(app);
const io = new Server(server);

const users = {}; // shared map[socketID] -> name

app.use(express.static(__dirname + "/public"));

app.get("/", (req, res) => {
  res.sendFile(__dirname + "/public/index.html");
});

io.on("connection", (socket) => {
  socket.on("new user", (name) => {
    users[socket.id] = name;
    io.emit("user connected", socket.id, name);
  });

  socket.on("new message", (socketId, msg) => {
    io.emit("chat message", socketId, users[socketId], msg);
  });

  socket.on("disconnect", () => {
    io.emit("user disconnect", socket.id, users[socket.id]);
    delete users[socket.id];
  });
});

server.listen(3000);
```

---
# Additional

[[Web Sockets Simplified]]
[[Web Sockets React]]
