#nodejs

Suppose we want to send a large file from server to client. We can simply readFile and res.send() it. But that will take a shit ton of memory.

And if no. of users were to increase, the load on server's ram will increase and server will eventually crash. Which isn't ideal.

A solution could be to **stream** the data by **chunks** instead. And read it as it loads.

Like a youtube video. We aren't waiting for the entire video to download and then watch it. We stream the video instead.

---
NodeJS supports streaming

```javascript
const { pipeline } = require('node:stream/promises');
const fs = require('node:fs');
const zlib = require('node:zlib');

async function run() {
  await pipeline(
    fs.createReadStream('archive.tar'),
    zlib.createGzip(),
    fs.createWriteStream('archive.tar.gz'),
  );
  console.log('Pipeline succeeded.');
}

run().catch(console.error);
```

- [`Writable`]: streams to which data can be written
- [`Readable`]: streams from which data can be read

Here we are reading, zipping and then writing chunks on stream them without much memory consumption on server.
