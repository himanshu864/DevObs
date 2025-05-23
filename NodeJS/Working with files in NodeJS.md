#nodejs 

```js
const fs = require("fs");
console.log(fs);
```

To synchronously create file with content. Returns result

```js
fs.writeFileSync("himanshu.txt", "Himanshu joined as an intern!");
```

Better use async. expects callback with error and result

```js
console.log("start"); // 1
fs.writeFile("himanshu.txt", "Himanshu joined as an intern!", (err, res) => {
    console.log("done") // 3
});
console.log("end"); // 2
```

To read file at exists

```js
fs.readFile("himanshu.txt", (error, data) => {
    console.log(error, data.toString());
});
```

To append to a file that exists

```js
fs.appendFile("./NodeJS//himanshu.txt", "\\nand he's great", (e, d) => {
    console.log(d);
})
```

To the same using promise to avoid callback hell

```js
const fs = require("fs/promises");
import fs from "fs/promises";

let a = await fs.writeFile("./NodeJS/02-fs-path/harry.txt", "this is good");

let c = await fs.appendFile("./NodeJS/02-fs-path/harry.txt", "\\nAh that's good!");

let b = await fs.readFile("./NodeJS/02-fs-path/harry.txt");
console.log(b.toString());
```

- `path.js`

```js
import path from "path";

// console.log(path);

const myPath = "/home/artoriax/WebDev/NodeJS/02-fs-path/harry.txt";

console.log(path.extname(myPath));
console.log(path.dirname(myPath));
console.log(path.basename(myPath));

// console.log(path.join("/home/sef", "sad\\\\asdf.txt"));
```

## Useful fs, fs/promise, path METHODS to clear Clutter
---

```js
import path, { extname } from "path";
import fs from "fs";
import promises from "fs/promises";

const root = "./NodeJS/Exercise";
const newFile = "/logs.txt";

// create file in root directory
await promises.writeFile(root + newFile, "It works!");

// find out extention name of file, and save it's path as folder
const folderPath = root + `/${path.extname(root + newFile)}`;

// to create organised folder if doesn't exists;
if (!fs.existsSync(folderPath))
    await promises.mkdir(folderPath, () => { });

// to copy file from parent to organized folder
await promises.copyFile(root + newFile, folderPath + newFile);

// read content of a directory
const files = await promises.readdir(root + "/Clutter");
for (const file of files) {
    console.log(file);
    //console.log(extname(file));
}

// delete files
fs.unlinkSync(root + '/temp.txt');

// create directories recursively
fs.mkdirSync(root + "/a/b/c", { recursive: true });
```
