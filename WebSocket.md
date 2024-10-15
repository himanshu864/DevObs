#nodejs 

Our usual client-server architecture works on request and response. Client requests to server. And server responds. And connection ends there~

But what if, server has a message of client? Then it's gonna have to wait until client requests again. Which is not ideal.

One thing we can do is to request sever every second to check of responses. Which is called **Polling**. And that is far more ideal. Too much burden on server. Overkill

another solution is
### Web-Sockets
- Computer communication protocol providing full-duplex communication.
- They basically update normal HTTP connection to Web Socket connection.

---
### Socket.io
Socket.IO is composed of two parts:

- A server that integrates with (or mounts on) the Node.JS HTTP Server (the [`socket.io`](https://www.npmjs.com/package/socket.io) package)
- A client library that loads on the browser side (the [`socket.io-client`](https://www.npmjs.com/package/socket.io-client) package)

- **app.js**
```javascript
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
- Initialise io (input/output) instance by passing server (HTTP) object
- Need to sendFile and not ejs for web sockets

- **/public/index.html**
```html
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
##### Emit
The main idea behind Socket.IO is that you can send and receive any events you want, with any data you want

- Take input from user
```javascript
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
On client-side. First sender sends message. And then we'll capture msg event and display it!
And with that, we have a working real-time chat application

---
- We can send anything and everything inside **socket.emit()**. Whether it be client to server or vice-versa
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

### Cheat sheet
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
