---
tags:
  - backend
references:
  - https://youtu.be/Vx2zPMPvmug?si=LjeHY6nCU9HnfwAK
date_created: 2025-06-15
date_modified: 2025-06-16
title: Redis
---
---

Redis is an in-memory key–value database, used as a distributed cache and message broker, with optional durability.

In-memory means redis keeps data in RAM. Thus, is very fast.

---
# Installation

Install on Docker to simulate production environment. We're gonna install `Redis-stack` for GUI visualization.

1. Install and run Docker
2. Run this command

```bash
docker run -d --name redis-stack -p 6379:6379 -p 8001:8001 redis/redis-stack:latest
```

Open `localhost:8001` on your browser to check if GUI is working.

3. Run this command to run bash inside container. `${container.id}`
```bash
docker exec -it 049ab0c2ce47 bash
```

4. Now run `redis-cli` command to interact with redis sever directly via terminal.

Type `ping` to check if everything is working.

---
# Redis String

- **SET** stores a string value
- **GET** retrieves a string value

```bash
set my_key my_value
# OK
get my_key
# my_value
```

- **SETNX** stores a string value only if the key doesn't already exist. Useful for implementing locks.

```bash
set my_key my_value_2 nx
# (nil)
```

- **MGET** retrieves multiple string values in a single operation.

```bash
mget my_key_1 my_key_2
# 1) my_value_1
# 2) my_value_2
```

### Managing counters

- **INCR** atomically increments counters stored at a given key by 1.
- **INCRBY** atomically increments (and decrements when passing a negative number) counters stored at a given key.

```bash
set counter 0
# OK
incr counter
# (integer) 1
incr counter
# (integer) 2
incrby counter 10
# (integer) 12
incrby counter -5
# (integer) 7
```

## Time to Live

To expire a key value pair after some time (seconds).

```bash
expire my_key 5
# (integer) 1
get my_key
# my_value
get my_key
# (nil)
```

---
# Run on NodeJS

1. Start a repository and run following commands

```bash
npm init -y
npm i ioredis
```

2. Create `client.js`

```js
const Redis = require("ioredis");

const client = new Redis();

module.exports = client;
```

3. Create `string.js`

```js
const client = require("./client");

async function func() {
  const val = await client.get("abhishek");
  console.log(val);
}

func();
```

Try and run `node string.js`. Similarly you can run all redis commands.

---
# Redis List

Redis lists are linked lists of string values. Redis lists are frequently used to:

- Implement stacks and queues.
- Build queue management for background worker systems.

### Basic Commands

- **LPUSH** adds a new element to the head of a list; **RPUSH** adds to the tail.
- **LPOP** removes and returns an element from the head of a list; **RPOP** does the same but from the tails of a list.
- **LLEN** returns the length of a list.
- **LMOVE** atomically moves elements from one list to another.
- **LRANGE** extracts a range of elements from a list.
- **LTRIM** reduces a list to the specified range of elements.

```bash
lpush messages msg1
# (integer) 1
lpush messages msg2
# (integer) 2
rpush messages msg3
# (integer) 3
lpop messages
# "msg2"
llen messages
# (integer) 1
```

### Blocking Commands

**BLPOP** removes and returns an element from the head of a list. If the list is empty, the command blocks until an element becomes available or until the specified timeout is reached.

```bash
blpop messages 10
# ...
lpush messages hello
# 1
# ... hello
```

If list is empty, BLPOP waits 10 seconds for someone to push something to the list.

### Range

- **LRANGE** returns list from start to stop.

```bash
lrange messages 0 -1
# 1) "msg1"
# 2) "msg3"
```

- **DEL** my_key: deletes `my_key`.
- **KEY** my_key\*: returns all keys starting with `my_key`.

---
# Redis sets

A Redis set is an unordered collection of unique strings (members). You can use Redis sets to efficiently:

- Track unique items (e.g., track all unique IP addresses accessing a given blog post).
- Represent relations (e.g., the set of all users with a given role).
- Perform common set operations such as intersection, unions, and differences.

- **SADD** adds a new member to a set.
- **SREM** removes the specified member from the set.
- **SISMEMBER** tests a string for set membership.
- **SINTER** returns the set of members that two or more sets have in common (i.e., the intersection).
- **SCARD** returns the size (a.k.a. cardinality) of a set.

```bash
sadd st s1
# (integer) 1
sadd st s2 s3 s4
# (integer) 3
sadd st s2
# (integer) 0
srem st s3
# (integer) 1
sismember st s1
# (integer) 1
sismember st s3
# (integer) 0
scard st
# (integer) 3
```

---
# Redis Hashes

Redis hashes are record types structured as collections of field-value pairs. You can use hashes to represent basic objects and to store groupings of counters, among other things.

- **HSET**: sets the value of one or more fields on a hash.
- **HGET**: returns the value at a given field.
- **HMGET**: returns the values at one or more given fields.
- **HINCRBY**: increments the value at a given field by the integer provided.

```bash
HSET bike:1 model Deimos brand Ergonom type 'Enduro bikes' price 4972
# (integer) 4
HGET bike:1 model
# "Deimos"
HGET bike:1 price
# "4972"
HGETALL bike:1
# 1) "model"
# 2) "Deimos"
# 3) "brand"
# 4) "Ergonom"
# 5) "type"
# 6) "Enduro bikes"
# 7) "price"
# 8) "4972"
```

NodeJS Server
```js
const res1 = await client.hSet(
  'bike:1',
  {
    'model': 'Deimos',
    'brand': 'Ergonom',
    'type': 'Enduro bikes',
    'price': 4972,
  }
)
```

---
# Redis Ordered Sets (Priority Queue)

A Redis sorted set is a collection of unique strings (members) ordered by an associated score. When more than one string has the same score, the strings are ordered lexicographically.

- **ZADD** adds a new member and associated score to a sorted set. If the member already exists, the score is updated.
- **ZRANGE** returns members of a sorted set, sorted within a given range.
- **ZRANK** returns the rank of the provided member, assuming the sorted is in ascending order.
- **ZREVRANK** returns the rank of the provided member, assuming the sorted set is in descending order.
- **ZINCRBY** adds points to existing score.

```bash
ZADD racer_scores 10 "Norem"
# (integer) 1
ZADD racer_scores 12 "Castilla"
# (integer) 1
ZADD racer_scores 8 "Sam-Bodden" 10 "Royce" 6 "Ford" 14 "Prickett"
# (integer) 4
ZRANGE racer_scores 0 -1
1) "Ford"
2) "Sam-Bodden"
3) "Norem"
4) "Royce"
5) "Castilla"
6) "Prickett"
```

---
# Redis Streams

A Redis stream is a data structure that acts like an append-only log but also implements several operations to overcome some of the limits of a typical append-only log. These include random access in O(1) time and complex consumption strategies, such as consumer groups. You can use streams to record and simultaneously syndicate events in real time.

- **XADD** adds a new entry to a stream.
- **XREAD** reads one or more entries, starting at a given position and moving forward in time.
- **XRANGE** returns a range of entries between two supplied entry IDs.
- **XLEN** returns the length of a stream.

---
# Redis Geospatial Data

Redis geospatial indexes let you store coordinates and search for them. This data structure is useful for finding nearby points within a given radius or bounding box.

- **GEOADD** adds a location to a given geospatial index (note that longitude comes before latitude with this command).
- **GEOSEARCH** returns locations with a given radius or a bounding box.

---
### Redis can also Pub-Sub

