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

Can pass complex data using query params.

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

