---
tags:
  - python
  - backend
references:
  - https://www.youtube.com/watch?v=iWS9ogMPOI0
date_created: 2025-07-24
date_modified: 2025-07-24
---
---
## Getting Started

1. Create a virtual environment and install dependencies.

```bash
pip3 install virtualenv
virtualenv venv
source venv/bin/activate

pip3 install fastapi
pip3 install uvicorn

# or

pip3 install "fastapi[standard]"
```

2. Create your hello world application

```python
# app.py
from fastapi import FastAPI

app = FastAPI()


@app.get("/")
def root():
    return {"Hello": "World"}
```

3. Run your application locally.

```bash
uvicorn app:app --reload

# or 

fastapi dev app.py
```

---
## Routes

```python
# temp database
items: List[str] = ["apple", "ball"]


@app.get("/items")
def get_items():
    return {"Items": items}


# postman or cURL (query params)
@app.post("/items")
def create_item(item: str):
    items.append(item)
    return items


# post using slugs
@app.post("/items/{item}")
def append_item(item: str):
    items.append(item)
    return {"Items": items}


@app.get("/items/{item_id}")
def get_item_by_id(item_id: int):
    item = items[item_id]
    return item
```

Test post using terminal

```bash
curl
	-X POST
	-H "Content-Type: application/json"
	'http://127.0.0.1:8000/items?item=himanshu'

# ["apple","ball","himanshu"]
```

---
## Exceptions

```python
from fastapi import FastAPI, HTTPException

# ...

@app.get("/items/{item_id}")
def get_item_by_id(item_id):
    try:
        return items[int(item_id)]
    except:
        raise HTTPException(status_code=404, detail=f"Item {item_id} not found")
```

---
## Class and JSON requests

Can pass complex data using query params. Use [[Pydantic]] for model validation.

```python
from pydantic import BaseModel

class Item(BaseModel):
    text: str = None
    is_done: bool = False


items: List[Item] = [{"text": "OS"}, {"text": "CN"}]


@app.get("/items")
def get_items():
    return {"Items": items}


# Query Params only
@app.post("/items")
def create_item(item: Item):
    items.append(item)
    return items
```

Test using terminal cURL

```bash
curl
	-X POST
	-H "Content-Type: application/json"
	-d '{"text": "DBMS"}'
	'http://127.0.0.1:8000/items'
# [{"text":"OS"},{"text":"CN"},{"text":"DBMS","is_done":false}]
```

---
## Lifespan

For events like connecting to database or loading machine learning model, that needs to be run at the start of the application and close with it, you can use **Lifespan** feature of FastAPI.

```python
from contextlib import asynccontextmanager
from fastapi import FastAPI

@asynccontextmanager
async def lifespan(app: FastAPI):
    # connect to database
    yield
    # disconnect to database

app = FastAPI(lifespan=lifespan)
```

---
## Logs

```python
import logging

logger = logging.getLogger("uvicorn.error")
logger.setLevel(logging.DEBUG)

@app.get("/")
async def root():
    loggerdebug("Server is running")
    return {"message": "Server is running"}
```

---
## Integrating Redis

0. Refer to [[Redis]] for basic knowledge and install dependencies

```bash
pip3 install redis
pip3 install aioredis
```

0. Start a docker container

```yaml
services:
  redis:
    image: redis:7-alpine
    restart: always
    volumes:
      - ./redis_data:/data
    healthcheck:
      test: ["CMD", "redis-cli", "ping"]
      interval: 10s
      timeout: 5s
      retries: 5
```

2. Create a redis instance `src/redis.py`.

```python
import os
import redis.asyncio as redis

redis_host = os.getenv("REDIS_HOST", "localhost")

redis_url = f"redis://{redis_host}:6379"

redis = redis.from_url(
    redis_url,
    decode_responses=True,
)
```

3. Start using using async redis in your application

```python
from src.redis import redis

@asynccontextmanager
async def lifespan(app: FastAPI):
    isRedisAlive = await redis.ping()
    if isRedisAlive:
        logger.debug("Successfully connected to Redis")

    yield
    await redis.close()
    logger.debug("Successfully disconnected from Redis!")


@app.get("/user/{user_id}", response_model=UserResponse)
async def get_user_by_id(user_id: str):
    # 1. Check cache
    cached_user = await redis.get(user_id)
    if cached_user:
        logger.debug(f"Cache HIT for user:{user_id}")
        return UserResponse.model_validate_json(cached_user)

    # 2. If not cache, query database
    user = await prisma.user.find_unique(where={"id": user_id})
    if not user:
        raise HTTPException(status_code=404, detail="User not found")

    # 3. Cache user
    user_response = UserResponse.model_validate(user)
    await redis.set(user_id, user_response.model_dump_json(), ex=300)

    return user_response

```

---
