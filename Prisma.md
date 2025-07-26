---
tags:
  - backend
  - docker
  - dbms
references:
  - https://youtu.be/RebA5J-rlwg?si=cjRJMJ8dqVDP394s
date_created: 2025-07-21
date_modified: 2025-07-21
---
---
# Installation

### Prerequisites

Before you begin, make sure you have the following installed:

- **Node.js**: The JavaScript runtime environment.
- **Docker Desktop**: The application for building and running containerized applications.

### Set Up the PostgreSQL Container

We'll use `docker-compose` to define and run our PostgreSQL service. It simplifies managing container settings.

1. **Create a Project Directory**

Create a new folder for your project and navigate into it.

```bash
mkdir my-prisma-project
cd my-prisma-project
```

2. **Create a `docker-compose.yml` File**

Inside your project folder, create a file named `docker-compose.yml` and add the following content:

```yaml
services:
  db:
	image: postgres:15 # Use a specific postgres version
	restart: always
	environment:
	  POSTGRES_USER: myuser
	  POSTGRES_PASSWORD: mypassword
	  POSTGRES_DB: mydb
	ports:
	  - '5432:5432' # Map container port to host port
	volumes:
	  - ./postgres_data:/var/lib/postgresql/data
```

- **`environment`**: Sets the username, password, and initial database name.
- **`ports`**: Exposes the PostgreSQL port `5432` from the container to your local machine.
- **`volumes`**: Persists your database data in a `postgres_data` folder, so you don't lose it when the container stops.

3. **Start the Container**

Open your terminal in the project directory and run:

```bash
docker-compose up -d
```

The `-d` flag runs the container in detached mode (in the background). Your PostgreSQL database is now running!

### Initialize Your Prisma Project

Now, let's set up a NodeJS project and add Prisma to it.

1. **Initialize a Node.js Project**

```bash
npm init -y
```

2. **Install Dependencies**

Install Prisma as a development dependency and Prisma Client as a regular dependency.

```bash
# Install dev dependencies
npm install prisma typescript ts-node @types/node --save-dev

# Install Prisma Client
npm install @prisma/client
```

3. **Initialize TypeScript**

Run `npx tsx --init` and refer following file.

```json
// tsconfig.json
{
  "compilerOptions": {
    /* Base Options */
    "esModuleInterop": true,
    "skipLibCheck": true,
    "target": "ES2022",
    "allowJs": true,
    "resolveJsonModule": true,
    "moduleDetection": "force",
    "isolatedModules": true,

    /* Strictness */
    "strict": true,
    "noUncheckedIndexedAccess": true,
    "forceConsistentCasingInFileNames": true,

    /* If you are building for a library */
    // "declaration": true,

    /* If you are building for a browser */
    // "lib": ["dom", "dom.iterable", "esnext"],

    /* Module settings for Node.js */
    "module": "NodeNext",
    "moduleResolution": "NodeNext",
    "rootDir": "src",
    "outDir": "dist",
    "sourceMap": true
  },
  "include": ["src/**/*.ts"],
  "exclude": ["node_modules"]
}
```

4. **Initialize Prisma**

Run the Prisma init command. This creates a prisma directory with a schema.prisma file and a .env file for your database connection string.

```bash
npx prisma init --datasource-provider postgresql
```

### Configure the Database Connection

1. **Update the .env File**

Open the newly created .env file and set the DATABASE_URL. This URL must match the credentials you set in your `docker-compose.yml` file.

```bash
# .env
DATABASE_URL="postgresql://myuser:mypassword@localhost:5432/mydb"
```

Prisma automatically loads variables from this file.

2. **Define a Data Model**

Open prisma/schema.prisma. It's already configured to use PostgreSQL. Now, let's add a simple model to define a database table.

```prisma
// prisma/schema.prisma

generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

model User {
  id Int @id @default(autoincrement())
  createdAt DateTime @default(now())
  email String @unique
  name String
}
```

### Migrate and Interact with the Database

1. **Run Your First Migration**

A migration syncs your Prisma schema with your database schema. The following command will create the User table in your Dockerised database.

```bash
npx prisma migrate dev --name init
```

Prisma will ask you to name the migration (we provided `init`). It will then generate the SQL and apply it to the database.

This generates a client that provides you all the necessary code to interact with the database, with type safety. To manually generate client, run following command.

```bash
npx prisma generate
```

- **`npx prisma migrate dev`**: This command **changes your database**. It compares your `schema.prisma` file to the actual database structure. If there are differences, it generates and runs a new SQL file to update the database tables, columns, etc. Think of it as **syncing your schema with the database**.
- **`npx prisma generate`**: This command **updates your application's code**. It reads your `schema.prisma` file and generates the `PrismaClient` library tailored to your models (`User`, `Post`, etc.). It gives you the TypeScript types and functions so your editor knows what `prisma.user.findUnique` means. Think of it as **syncing your schema with your code**.

> **Key takeaway**: `migrate` affects the database, while `generate` affects the code that talks to the database. Note that `prisma migrate dev` automatically runs `prisma generate` for you after a successful migration.

2. **Create a Script to Interact with the DB**

Export `prisma` throughout the application.

```ts
// src/lib/prisma.ts
import { PrismaClient } from '@prisma/client'

export const prisma = new PrismaClient()
```

Create a file named `index.ts` and add the following code to create a new user and then fetch all users.

```ts
// src/index.ts
import { prisma } from './lib/prisma'

async function main() {
  const newUser = await prisma.user.create({
    data: {
      name: 'Rahul',
      email: 'rahul@gmail.com',
    },
  })

  console.log(newUser)

  const allUsers = await prisma.user.findMany()
  console.log('All users: ')
  console.dir(allUsers, { depth: null })
}

main()
  .catch(async (e) => {
    console.error(e)
    process.exit(1)
  })
  .finally(async () => {
    await prisma.$disconnect()
  })
```

3. **Run the Script**

Add following scripts.

```json
// package.json
{
  "scripts": {
    "dev": "npx ts-node src/index.ts",
    "build": "npx tsc",
    "start": "node dist/index.js",
  },
}
```

And execute script.

```bash
npm run build
npm run start
```

You should see the output confirming that a user was created and then fetched from your database, which is running securely inside a Docker container.

---
# Model

> The core of Prisma is the `schema.prisma` file. It's the single source of truth for your database schema and application models. This guide breaks down its key components.
## Model Fields & Types

Each model in your schema represents a table in your database. Models are composed of fields, which represent the table's columns.

The basic syntax for a field is `fieldName FieldType @attributes`.

```prisma
model User {
  //  <field_name> <type> <@attributes>
  id             Int      @id @default(autoincrement())
  email          String   @unique
  name           String?  // The '?' makes this field optional
  posts          Post[]   // The '[]' denotes a list of relations
}
```

- **Field Modifiers**:
    - `?` (Optional): The field can be `null` in the database.
    - `[]` (List): Represents a "to-many" relationship. This does not create a native database array (unless the DB supports it), but rather connects to multiple related records.
- **Common Scalar Types**:
    - `String`: Variable-length text.
    - `Int`: 32-bit signed integers.
    - `BigInt`: For very large integers.
    - `Boolean`: `true` or `false`.
    - `Float`: Floating-point numbers (for representing decimals).
    - `Decimal`: For high-precision decimal numbers, ideal for financial calculations.
    - `DateTime`: Stores a date and time with time zone information.
    - `Json`: For storing JSON objects.
    - `Bytes`: For storing byte arrays.

## Model Relationships

Prisma makes defining complex relationships between models incredibly intuitive. It manages foreign keys and join tables for you.

#### One-to-One (1-to-1)

A user has one profile, and a profile belongs to one user.

```prisma
model User {
  id      Int      @id @default(autoincrement())
  profile Profile? // Optional: A user might not have a profile
}

model Profile {
  id     Int    @id @default(autoincrement())
  bio    String
  user   User   @relation(fields: [userId], references: [id])
  userId Int    @unique // Crucial: @unique enforces the 1-to-1 relationship
}
```

> **Key Insight**: The `@unique` constraint on the foreign key (`userId`) is what ensures a `Profile` can only be linked to one `User`.

#### One-to-Many (1-to-N)

A user can write many posts, but each post is written by only one user.

```prisma
model User {
  id    Int    @id @default(autoincrement())
  posts Post[] // A user can have a list of posts
}

model Post {
  id        Int      @id @default(autoincrement())
  title     String
  author    User     @relation(fields: [authorId], references: [id])
  authorId  Int      // This is the foreign key
}
```

A user can also have many favorite posts. i.e. Multiple one-to-many.

```prisma
model User {
  id String @id @default(uuid())
  createdAt DateTime @default(now())
  email String @unique
  name String
  writtenPosts Post[] @relation("WrittenPosts")
  favoritePosts Post[] @relation("FavoritedPosts")
}

model Post {
  id String @id @default(uuid())
  rating Float
  authorId String
  author User @relation("WrittenPosts", fields: [authorId], references: [id])
  favoritedById String
  favoritedBy User @relation("FavoritedPosts", fields: [favoritedById], references: [id])
}
```

#### Many-to-Many (M-to-N)

A post can have multiple categories, and a category can contain multiple posts.

```prisma
model Post {
  id         Int        @id @default(autoincrement())
  title      String
  categories Category[] // A post can have a list of categories
}

model Category {
  id    Int    @id @default(autoincrement())
  name  String
  posts Post[] // A category can have a list of posts
}
```

> **Magic ✨**: Prisma automatically creates and manages the hidden "join" or "lookup" table in the database for you. You don't need to define it in the schema.

---
## Attributes

Attributes modify the behavior of fields or models. They start with `@` for field-level attributes and `@@` for block-level (model-level) attributes.

- **`@id`**: Designates the field as the primary key for the model.
- **`@default(...)`**: Sets a default value. Common functions include `autoincrement()`, `now()`, and `uuid()`.
- **`@unique`**: Enforces that every value in this column must be unique.
- **`@updatedAt`**: Automatically updates a `DateTime` field to the current timestamp whenever the record is modified.
- **`@relation(...)`**: Explicitly defines the details of a relationship (foreign keys, referenced fields).
- **`@@id([...])`**: Creates a composite primary key from multiple fields.
- **`@@unique([...])`**: Creates a unique constraint across multiple fields. For example, a user's `firstName` and `lastName` combination must be unique.
- **`@@index([...])`**: Creates a database index on one or more fields to speed up queries.

```prisma
model UserPreference {
  id          Int      @id @default(autoincrement())
  emailUpdates Boolean  @default(true)
  user        User     @relation(fields: [userId], references: [id])
  userId      Int      @unique

  // Block-level attribute for a composite unique constraint
  @@unique([userId, id])
}
```

---
## Enums

Enums define a set of allowed values for a field, ensuring type safety and preventing invalid data. They are perfect for fields like roles, statuses, or types.

```prisma
// 1. Define the Enum
enum Role {
  BASIC
  EDITOR
  ADMIN
}

// 2. Use the Enum in a model
model User {
  id   Int  @id @default(autoincrement())
  role Role @default(BASIC) // The 'role' field can only be BASIC, EDITOR, or ADMIN
}
```

---
# Prisma Client CRUD Operations

Once your schema is defined, `npx prisma generate` creates a powerful, type-safe client that you can use to interact with your database. It's available via `import { PrismaClient } from '@prisma/client'`.

> **Best Practice**: Create a single, shared instance of `PrismaClient` for your entire application to avoid creating too many database connections.

### Creating a Single Record

Use `prisma.model.create()` to add a new record to the database.

```ts
const user = await prisma.user.create({
  data: {
    name: 'Alice',
    email: 'alice@prisma.io',
    age: 30,
  },
})
```

### Creating Related Records (Nested Create)

You can create a record and its related records in a single transaction.

```ts
const userWithProfile = await prisma.user.create({
  data: {
    name: 'Bob',
    email: 'bob@prisma.io',
    // Create a related UserPreference record at the same time
    userPreference: {
      create: {
        emailUpdates: true,
      },
    },
  },
  // You can also include the new related record in the response
  include: {
    userPreference: true,
  },
})
```

### Creating Multiple Records

Use `prisma.model.createMany()` to perform a bulk insert. It's much more efficient than creating records one by one in a loop.

```ts
const count = await prisma.user.createMany({
  data: [
    { name: 'Carol', email: 'carol@prisma.io', age: 25 },
    { name: 'Dave', email: 'dave@prisma.io', age: 28 },
  ],
})
// Returns a count of the records created
```

> **Note**: `createMany` does not support `include` or `select` clauses.

---
### Fetching a Single Record by ID or Unique Field

Use `prisma.model.findUnique()` for the fastest way to get a single record.

```ts
const user = await prisma.user.findUnique({
  where: {
    // Can use any field marked with @id or @unique
    email: 'alice@prisma.io',
  },
})
```

### Fetching the First Matching Record

Use `prisma.model.findFirst()` to get the first record that matches a set of criteria.

```ts
const userNamedAlice = await prisma.user.findFirst({
  where: {
    name: 'Alice',
  },
})
```

### Fetching Multiple Records

Use `prisma.model.findMany()` to get a list of all records matching a filter.

```ts
const allUsers = await prisma.user.findMany({
  // An empty where clause fetches all records
})

const usersOver25 = await prisma.user.findMany({
  where: {
    age: {
      gt: 25, // 'gt' means "greater than"
    },
  },
})
```

---
## Advanced Filtering & Sorting

You can build complex queries using a rich set of operators within the `where` clause.

- **Filtering Operators**:
    - Equality: `equals`, `not`
    - Range: `lt` (less than), `lte`, `gt` (greater than), `gte`
    - Membership: `in: [...]`, `notIn: [...]`
    - String: `contains`, `startsWith`, `endsWith` (case-sensitive by default)
- **Logical Operators**: Combine filters with `AND`, `OR`, and `NOT`.

```ts
const specificUsers = await prisma.user.findMany({
  where: {
    OR: [
      { name: { startsWith: 'A' } },
      {
        AND: [
            { email: { contains: 'prisma.io' } },
            { age: { gte: 30 } }
        ],
      },
    ],
  },
  // Sort results by age in descending order
  orderBy: {
    age: 'desc',
  },
  // Paginate results: get 10 records, skipping the first 20
  take: 10,
  skip: 20,
})
```

### Relationship Filtering

Filter records based on the properties of their related models.

- `some`: At least one related record matches the filter.
- `every`: All related records match the filter.
- `none`: No related records match the filter.

```ts
// Find all users who have written at least one post with "TypeScript" in the title
const authors = await prisma.user.findMany({
  where: {
    posts: {
      some: {
        title: {
          contains: 'TypeScript',
        },
      },
    },
  },
})
```

---
### Updating a Single Record

Use `prisma.model.update()` to modify a single record, identified by a unique field.

```ts
const updatedUser = await prisma.user.update({
  where: {
    email: 'alice@prisma.io',
  },
  data: {
    age: 31,
  },
})
```

### Connecting Existing Relationships

Instead of creating a new related record, you can use `connect` to link to an existing one.

```ts
const updatedUser = await prisma.user.update({
  where: { email: 'bob@prisma.io' },
  data: {
    // Connect this user to an existing preference record
    userPreference: {
      connect: {
        id: 'some-preference-id', // ID of the preference record
      },
    },
  },
})
```

You can also `disconnect` relations in the same way.

### Atomic Number Operations

Update numbers safely without reading the value first.

increment, decrement, multiply, divide, set.

```ts
const user = await prisma.user.update({
  where: { email: 'alice@prisma.io' },
  data: {
    age: {
      increment: 1, // Atomically increments the age by 1
    },
  },
})
```

---
### Deleting a Single Record

Use `prisma.model.delete()` to remove a single record, identified by a unique field.

```ts
const deletedUser = await prisma.user.delete({
  where: {
    email: 'dave@prisma.io',
  },
})
```

### Deleting Multiple Records

Use `prisma.model.deleteMany()` to remove all records matching a `where` clause.

```ts
const result = await prisma.user.deleteMany({
  where: {
    age: {
      lt: 20, // Delete all users younger than 20
    },
  },
})
// Returns a count of deleted records
```

> Warning: deleteMany() is powerful. To delete all records in a table, you can pass an empty where clause: prisma.user.deleteMany({}). Use with caution!
