#backend #nodejs  

This is detailed guide following Web Dev Simplified youtube video. Explains concepts like join rooms and handling admin dashboards.
## Boilerplate

#### Server

1. Perform these steps in the root directory of your project.

```bash
mkdir server
cd server
touch server.js
npm init -y
npm i express nodemon socket.io
```

2. And paste this boilerplate code inside `server.js`. Shorthand for creating a Socket.IO server with an internal HTTP server listening on port 3000. And CORS configuration to allow requests from client server.

```javascript
const io = require("socket.io")(3000, {
  cors: {
    origin: "http://localhost:8080",
  },
});

io.on("connection", (socket) => {
  console.log("User connected!");

  socket.on("disconnect", () => {
    console.log("User disconnected!");
  });
});
```

3. Run this server. (add `npm start` script)

#### Client (via snowpack and CDN)

1. Start by creating a `client` folder inside root directory and enter it.
2. Create an `index.html` with this basic html and css.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Socket.IO Chat Room</title>
    <style>
      body {
        margin: 0;
        padding-bottom: 3rem;
        font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
          Helvetica, Arial, sans-serif;
      }

      #messages-list {
        list-style-type: none;
        margin: 0;
        padding: 0;
        margin-bottom: 4rem;
      }

      #messages-list > li {
        padding: 0.5rem 1rem;
      }

      #messages-list > li:nth-child(odd) {
        background: #efefef;
      }

      form {
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

      label {
        padding-top: 0.5rem;
      }

      input {
        border: none;
        padding: 0 1rem;
        flex-grow: 1;
        border-radius: 2rem;
        margin: 0.25rem;
        margin-left: 2rem;
      }

      input:focus {
        outline: none;
      }

      form > button {
        background: #333;
        border: none;
        padding: 0 1rem;
        margin: 0.25rem;
        border-radius: 3px;
        outline: none;
        color: #fff;
      }

      #message-form {
        margin-bottom: 3rem;
      }

      #message-input {
        margin-left: 0.5rem;
      }
    </style>
  </head>

  <body>
    <ul id="messages-list"></ul>

    <form id="message-form">
      <label for="message-input">Message</label>
      <input type="text" id="message-input" />
      <button type="submit" id="send-button">Send</button>
    </form>
    <form id="room-form">
      <label for="room-input">Room</label>
      <input type="text" id="room-input" />
      <button type="submit" id="room-button">Join</button>
    </form>

    <script src="https://cdn.socket.io/4.6.1/socket.io.min.js"></script>
    <script src="script.js" type="module"></script>
  </body>
</html>
```

3. And create and link this `script.js` file inside the same directory.

```javascript
const socket = io("http://localhost:3000");

const messagesList = document.getElementById("messages-list");
const messageForm = document.getElementById("message-form");
const roomForm = document.getElementById("room-form");
const messageInput = document.getElementById("message-input");
const roomInput = document.getElementById("room-input");

const appendMessage = (msg) => {
  const item = document.createElement("li");
  item.textContent = msg;
  messagesList.appendChild(item);
  window.scrollTo(0, document.body.scrollHeight);
};

messageForm.addEventListener("submit", (event) => {
  event.preventDefault();
  if (!messageInput) return;

  appendMessage(`You: ${messageInput.value}`);
  messageInput.value = "";
  messageInput.focus();
});

roomForm.addEventListener("submit", (event) => {
  event.preventDefault();
  const room = roomInput.value;
  if (!room) return;

  roomInput.value = "";
  roomInput.focus();
});
```

4. Open terminal inside this client project and install `snowpack` dependency to build and run client server.

```bash
npm install --save-dev snowpack
```

5. Add common script to created `package.json` and run the client server as well.

```json
{
  "scripts": {
    "start": "snowpack dev",
    "build": "snowpack build"
  },
  "devDependencies": {
    "snowpack": "^3.8.8"
  }
}
```

By now you should have a proper client-server web socket connection and be able to emit and listen to events (signals).

> [!Note]
> Here I am loading `socket.io-client` library from CDN. But you also `npm` install this library. But right now I couldn't because it's clashing with `snowpack` library.

#### Client (via Express and `npm` library)

1. Perform these commands from your root directory.

```bash
mkdir client
cd client
touch client.js
npm init -y
npm i express socket.io-client
```

2. Paste following code inside `client.js`.

```javascript
const express = require("express");
const path = require("path");
const app = express();

app.use(express.static("public"));

app.use(
  "/socket.io-client",
  express.static(
    path.join(__dirname, "node_modules", "socket.io-client", "dist")
  )
);

app.listen(8080);
```

3. Create a new folder inside client named `public` and add `index.html` with `script.js` file inside it.

```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Socket.IO Chat Room</title>
    <style>
    </style>
    <script src="script.js" type="module"></script>
  </head>

  <body>
    <ul id="messages-list"></ul>

    <form id="message-form">
      <label for="message-input">Message</label>
      <input type="text" id="message-input" />
      <button type="submit" id="send-button">Send</button>
    </form>
    <form id="room-form">
      <label for="room-input">Room</label>
      <input type="text" id="room-input" />
      <button type="submit" id="room-button">Join</button>
    </form>
  </body>
</html>
```

```javascript
// script.js
import { io } from "/socket.io-client/socket.io.esm.min.js";
const socket = io("http://localhost:3000");

const messagesList = document.getElementById("messages-list");
const messageForm = document.getElementById("message-form");
const roomForm = document.getElementById("room-form");
const messageInput = document.getElementById("message-input");
const roomInput = document.getElementById("room-input");

const appendMessage = (msg) => {
  const item = document.createElement("li");
  item.textContent = msg;
  messagesList.appendChild(item);
  window.scrollTo(0, document.body.scrollHeight);
};

messageForm.addEventListener("submit", (event) => {
  event.preventDefault();
  if (!messageInput) return;

  appendMessage(`You: ${messageInput.value}`);
  messageInput.value = "";
  messageInput.focus();
});

roomForm.addEventListener("submit", (event) => {
  event.preventDefault();
  const room = roomInput.value;
  if (!room) return;

  roomInput.value = "";
  roomInput.focus();
});
```

4. Now run client server and verify web sockets connection.

---
## Rooms

After adding basic user connection, message and disconnection events on both sides (following [[WebSocket]] tutorial) we can start to work with rooms.

By default every socket has their own room, which is their `socket.id`.

Which means you can sent **private messages** using their Room ID i.e. socket id.

#### Private Messaging

1. Add a new input label inside message form in `index.html`.

```html
    <form id="message-form">
      <label for="message-input">Message</label>
      <input type="text" id="message-input" />
      <label for="private-room">Private Room (Blank for public)</label>
      <input type="text" id="private-room" />
      <button type="submit" id="send-button">Send</button>
    </form>
```

2. Send private Room ID along with message client-side `script.js`.

```javascript
messageForm.addEventListener("submit", (event) => {
  event.preventDefault();
  const message = messageInput.value;
  const privateId = privateRoomInput.value;
  if (!message) return;

  socket.emit("new-message", message, privateId);
  appendMessage(`You: ${message}`);
  messageInput.value = "";
  messageInput.focus();
});
```

3. Modify message listen server-side and send privately using `socket.to(root).emit()`.

```javascript
socket.on("new-message", (msg, room) => {
  if (!room) socket.broadcast.emit("chat-message", user[socket.id], msg);
  else socket.to(room).emit("chat-message", user[socket.id], msg);
});
```

#### Join Rooms

Now we can use our second form to join rooms.

```javascript
// script.js
roomForm.addEventListener("submit", (event) => {
  event.preventDefault();
  const room = roomInput.value;
  if (!room) return;

  socket.emit("join-room", room);
  roomInput.value = "";
  roomInput.focus();
});
```

```javascript
// server.js
  socket.on("join-room", (room) => {
    socket.join(room);
  });
```

One socket can join multiple rooms (including its own) and can send message to several rooms at a time.

#### Leave

To leave a channel you call `leave` in the same fashion as `join`.

- We then trigger a callback to immediately inform the user they've left.
- Finally, we notify everyone else in the room by emitting a "room-message" with a simple "Left" message. This ensures both the leaver and the remaining room members are kept in the loop.

```javascript
socket.on("leave-room", (room, cb) => {
  socket.leave(room);
  cb(`You left Room with ID : ${room}`);
  socket.to(room).emit("room-message", user[socket.id], room, "Left");
});
```

---
## Callback function

Client can emit function (always last argument) as callback function. To which Server can callback can respond after listening.

```javascript
// script.js
roomForm.addEventListener("submit", (event) => {
  event.preventDefault();
  const room = roomInput.value;

  socket.emit("join-room", room, (msg) => {
    appendMessage(msg);
  });
});
```

```javascript
// server.js
  socket.on("join-room", (room, cb) => {
    socket.join(room);
    cb(`You joined a Room with ID : ${room}`);
  });
```

---
## Admin UI

1. Install library inside server directory.
```bash
npm i @socket.io/admin-ui
```

2. Add instrument to `server.js`
```javascript
const { instrument } = require("@socket.io/admin-ui");
const io = require("socket.io")(3000, { 
/*...*/
instrument(io, { auth: false });
```

3. Whitelist `https://admin.socket.io/`
```javascript
const io = require("socket.io")(3000, {
  cors: {
    origin: ["http://localhost:8080", "https://admin.socket.io"],
    credentials: true,
  },
});
```

4. Visit [Admin UI](https://admin.socket.io/) website and enter `http://localhost:3000` as server URL to get an overview dashboard.

---

The reference video still has an introduction to concepts like
- namespaces (routing)
- middleware (authentications and errors)
- disconnecting and reconnecting (offline / volatile)

You can watch the video or read documentation to cover the rest. But for basic purposes, this tutorial should be enough.

---
## Misc

**Get all sockets inside a room**

```javascript
// server.js
  socket.on("join-room", async (room, cb) => {
    const sockets = await io.in(room).fetchSockets(); // <-
    if (sockets.length == 2) return;

    socket.join(room);
    cb(`You joined a Room with ID : ${room}`);
    socket.to(room).emit("room-message", user[socket.id], room, "Joined");
  });
```

