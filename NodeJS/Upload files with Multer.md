#nodejs 

- Set up boilerplate nodeJS with ejs and install `Multer`.
- **home.ejs**

```html
<form action="/profile" method="post" enctype="multipart/form-data">
  <input type="file" name="profileImage" />
  <button type="submit">Upload</button>
</form>
```

- `enctype` necessary for file upload
- **server.js**

```jsx
const express = require("express");
const app = express();

const multer = require("multer");

const storage = multer.diskStorage({
  destination: function (req, file, cb) {
    // callback returns (error, where to store uploaded file)
    return cb(null, "./uploads");
  },
  filename: function (req, file, cb) {
    // configure unique file name for no overiding
    return cb(null, Date.now() + "-" + file.originalname);
  },
});

// upload instance
const upload = multer({ storage });

app.set("view engine", "ejs");

app.use(express.urlencoded({ extended: false }));

// main router // Upload single for a single uploaded file
app.post("/upload", upload.single("profileImage"), (req, res) => {
  console.log(req.file);
  res.redirect("/");
});

app.get("/", (req, res) => {
  res.render("home.ejs");
});

app.listen(3000);
```

- Use disk storage to actually be able to view uploaded file on server
- Need to create uploads beforehand

