---
tags:
  - "#python"
  - backend
references: []
date_created: 2025-07-26
date_modified: 2025-07-26
---
---

Setup [[FastAPI]] and Postgres container by refer to [[Prisma]] before moving forward.

1. Install dependencies.

```bash
pip3 install prisma
```

2. Create schema file.

```prisma
// prisma/schema.prisma

datasource db {
  provider = "postgresql"
  url      = env("DB_URL")
}

generator client {
  provider             = "prisma-client-py"
  recursive_type_depth = 5
}

model User {
  id   String @id @default(uuid())
  name String
}
```

3. Define environment variables. `.env`

```
DB_URL="postgresql://artoriax:mypassword@localhost:5432/news_db"
```

4. Migrate database

```bash
prisma migrate dev --name init
```

5. Export a prisma instance

```python
# src/prisma.py

from prisma import Prisma

prisma = Prisma()
```

6. Connect to prisma and use this boilerplate to start developing.

```python
# main.py
from contextlib import asynccontextmanager
from fastapi import FastAPI
from src.prisma import prisma
import logging

logger = logging.getLogger("uvicorn.error")
logger.setLevel(logging.DEBUG)


# connect to db during lifecycle of the application
@asynccontextmanager
async def lifespan(app: FastAPI):
    await prisma.connect()
    logger.debug("Successfully connected to database!")

    yield
    await prisma.disconnect()
    logger.debug("Successfully disconnected from database!")


app = FastAPI(lifespan=lifespan)


@app.get("/")
async def root():
    return {"message": "Server is running"}


@app.get("/users")
async def get_users():
    users = await prisma.user.find_many()
    return {"users": users}
```

7. Test your application by running

```bash
fastapi dev main.py
```

And you're done. Happy development.

> [!error]
> Intellisense might not work, refer to following [documentation](https://prisma-client-py.readthedocs.io/en/stable/reference/operations/) for queries.

