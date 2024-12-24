#nodejs 

```bash
npm init -y
npm i express bcrypt
# touch .gitignore for node_modules
# set npm start to nodemon server.js
# use postman for handling API's
```

- **server.js :** Starting template for storing and displaying users on server

```js
const express = require("express");
const app = express();

const users = [];

app.get('/users', (req, res) => {
    res.json(users);
})

app.listen(3000);
```

- Need to create a POST request to create users and store them inside `users`

```js
app.post('/users', (req, res) => {
    const user = { name: req.body.name, password: req.body.password };
    users.push(user);
    res.status(201).send();
})
```

- Use Postman : POST: [*localhost:3000/users](http://localhost:3000/users) > Body > raw > JSON and enter user data to test*

```json
{
    "name": "Himanshu",
    "password": "password"
}
```

- This works fine but password is visible in plain text. Need to hash using `bcrypt`
- We need to add `salt` to our passwords before hashing them, so that multiple with password don’t end up with same encryptions. Salt will be different each time for each user.
- bcrypt takes care of that 😃

```js
const salt = await bcrypt.genSalt(); // cost of creating salt; default 10
const hashedPassword = await bcrypt.hash(req.body.password, salt);

console.log(salt);
console.log(hashedPassword);
```

or simply pass 10 to bcrypt.hash.

```js
app.post('/users', async (req, res) => {
    try {
        const hashedPassword = await bcrypt.hash(req.body.password, 10);
        const user = { name: req.body.name, password: hashedPassword };
        users.push(user);
        res.status(201).send();
    }
    catch {
        res.status(500).send();
    }
})
```

- To authenticate user, find user and `bcrypt.compare`

```js
app.post('/users/login', async (req, res) => {
    const user = users.find(user => user.name === req.body.name);
    if (user == null)
        return res.status(400).send('User does not exist');

    try {
        if (await bcrypt.compare(req.body.password, user.password)) {
            res.send('Logged In!');
        } else {
            res.send('Incorrect Password!');
        }

    } catch {
        res.status(500).send();
    }
})
```

# Voila! You’re done.
