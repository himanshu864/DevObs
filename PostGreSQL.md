---
tags:
  - backend
references:
  - https://youtu.be/cnzka7kF5Zk?si=fDIy2u5ykFJl1G0N
date_created: 2025-03-17
date_modified: 2025-03-17
---
---
## Installation

- Download installer from [website](https://www.enterprisedb.com/downloads/postgres-postgresql-downloads). Everything default. Set a simple password. Install.
- Open `pgAdmin4` and enter password after clicking on Server.

**Mac CLI**
Open `SQL Shell (psql).app` and enter for default and type password.

```sql
-- ctrl + L to clear terminal
\?    -- help
\l    -- list databases
CREATE DATABASE test;
\c test    -- connect to database test
\q    -- exit
```

**pgAdmin4**
- Go to `Servers > PostGreSQL > Databases > postgres` and click on query tool.
- Now you can query and get results using this interface.
- Right click on Databases to create new database. (or using SQL command in psql.app).
- Clicking on databases makes you connect. Can query or disconnect individually by right clicking.

```sql
SELECT datname FROM pg_database; -- display all db names
DROP DATABASE test;
```

