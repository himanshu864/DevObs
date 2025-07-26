#nodejs

Clusters of Node.js processes can be used to run multiple instances of Node.js that can distribute workloads among their application threads. When process isolation is not needed, use the `worker_threads` module instead, which allows running multiple application threads within a single Node.js instance.

The cluster module allows easy creation of child processes that all share server ports.

```javascript
const cluster = require("cluster");
const os = require("os");
const process = require("process");
const app = require("express")();

const numCPUs = os.cpus().length;

if (cluster.isPrimary) {
  console.log(`Primary ${process.pid} is running`);

  // Fork workers.
  for (let i = 0; i < numCPUs; i++) {
    cluster.fork();
  }
} else {
  app.get("/", (req, res) => {
    res.writeHead(200);
    res.end("hello world\n");
  });

  app.listen(8000);
  console.log(`Worker ${process.pid} started`);
}
```

Running Node.js will now share port 8000 between the workers:

```
$ node server.js  

Primary 1748098 is running
Worker 1748105 started
Worker 1748107 started
Worker 1748106 started
Worker 1748114 started
Worker 1748113 started
Worker 1748132 started
Worker 1748120 started
Worker 1748131 started
```

Now you can scale your NodeJS without crashing server.