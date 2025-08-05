---
tags:
  - "#next"
  - "#frontend"
references:
  - https://youtu.be/_EgI9WH8q1A?si=XnZPDWWIoIGSHyFq
date_created: 2025-03-29
date_modified: 2025-04-01
---
---

## What is NextJS?

NextJS is a full‑stack [[React]] framework designed to build production-ready web applications. It streamlines building both client- and server-side functionality with built-in support for routing, rendering, data fetching, and more.

- **Built on React:** Uses React for building user interfaces.
- **Full‑stack Capabilities:** Combines server-side rendering (SSR), static generation, and API routes.
- **Opinionated Conventions:** Encourages best practices with built‑in conventions and file‑based routing.
- **Additional Features:** Includes optimized performance, incremental static regeneration (ISR), middleware, image optimization, and SEO-friendly defaults.

---
## React Components in NextJS

### Server Components (Default)

- **Rendered on the server:** Sends pre-rendered HTML for faster first load.
- **Data fetching-friendly:** Ideal for retrieving data and interacting with secure backend resources.
- **No client-only hooks:** Cannot use `useState`, `useEffect`, or browser APIs.
- **Security:** Keeps sensitive logic and credentials off the client.

### Client Components

- **Rendered on the client:** Enables dynamic and interactive UIs.
- **Client-side hooks allowed:** Supports `useState`, `useEffect`, and other browser-only APIs.
- **Opt‑in:** Add `"use client"` at the top of the file to designate a client component.
- **Initial SSR:** Gets rendered to HTML once on the server for faster perceived performance.

---
## Routing

NextJS uses a file‑based routing system.

1. All routes must be placed inside the `App` folder.
2. Every folder corresponds to a path segment in browser URL.
3. Every file that represents a route must be named `page.tsx`.

> [!Tip]
> 1. **Dynamic Routes**: Create a folder named `[id]` and access it via *params*.
> 2. **Route Bundling:** Use parentheses (e.g. `(example)`) to group related routes without changing the URL.

---
## Layouts

- Allows you to define UI that is shared between multiple pages. Eg: navbar, sidebar, etc.
- When navigating between pages that share a layout, only the page components update - the layout doesn't re-render.
- Reduces code duplicated, improved structure, better performance, smoother user experience.

Layouts passes children prop which is `page.tsx` and everything else remains the same.

---
## Navigation

For internal links, NextJS recommends using its built‑in `<Link>` component, which offers faster client-side navigation and prefetching:

```tsx
// components/Navigation.tsx
"use client";
import Link from "next/link";
import { usePathname } from "next/navigation";

export const Navigation = () => {
  const pathname = usePathname();

  return (
    <nav>
      <Link href="/about" className={pathname === "/about" ? "font-bold" : ""}>
        About
      </Link>
      <Link href="/product/1" className={pathname.startsWith("/product") ? "font-bold" : ""}>
        Product 1
      </Link>
    </nav>
  );
};
```

And for programmatic navigation:

```tsx
// about/page.tsx
"use client";
import { useRouter } from "next/navigation";

export default function About() {
  const router = useRouter();
  return (
    <>
      <h1>About</h1>
      <button onClick={() => router.push("/")}>Go Home</button>
    </>
  );
}
```

---
## Route Handlers

NextJS allows you to create API endpoints with route handlers:

```tsx
// users/route.ts
export const users = [];

export async function GET() {
  return Response.json(users);
}

export async function POST(request: Request) {
  const user = await request.json();
  users.push(user);
  return new Response(JSON.stringify(user), {
    headers: { "Content-Type": "application/json" },
    status: 201,
  });
}
```

For dynamic API routes:

```tsx
// users/[id]/route.ts
import { users } from "../route.ts";

export async function GET(
  _request: Request,
  { params }: { params: { id: string } }
) {
  const user = users.find(user => user.id === parseInt(params.id));
  return Response.json(user);
}
```

---
## Data Fetching

NextJS differentiates data fetching between client and server components:

- **Client Components:** Use `useState`, `useEffect`, and similar hooks to fetch data. You’ll need to manage loading and error states manually.
- **Server Components:** Fetch data directly in the component with `await` syntax. NextJS automatically handles caching, errors, and loading states when you provide `error.tsx` and `loading.tsx` files.

```tsx
// users-server/page.tsx
type User = { id: number; name: string };

export default async function UsersServer() {
  const response = await fetch("https://backend-url.com");
  const users = await response.json();
  return <>{users.map((user: User) => <div key={user.id}>{user.name}</div>)}</>;
}
```

Automatic error and loading UIs:

```tsx
// users-server/error.tsx
"use client";
export default function Error({ error }: { error: Error }) {
  return <div>Error: {error.message}</div>;
}
```

```tsx
// users-server/loading.tsx
export default function Loading() {
  return <div>Loading users...</div>;
}
```

---
## Server Actions

Asynchronous functions that are executed on server. Useful for data mutation and form submissions.

1. Add input form with action `addUser` server function.
2. Get `name` input value from `FormData` argument.
3. POST that `name` to API and `revalidatePath` to update page automatically.

```tsx
// src/app/mock-users/page.tsx
import { revalidatePath } from "next/cache";

type MockUser = { id: number; name: string };

export default async function Users() {
  const res = await fetch("https://mockapi.io/users");
  const users = await res.json();

  async function addUser(formData: FormData) {
    "use server";
    const name = formData.get("name");
    await fetch("https://mockapi.io/users", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({ name }),
    });
    revalidatePath("/mock-users");
  }

  return (
    <div>
      <form action={addUser}>
        <input type="text" name="name" required />
        <button type="submit">Add User</button>
      </form>
      <div>
        {users.map((user: MockUser) => (
          <div key={user.id}>{user.name}</div>
        ))}
      </div>
    </div>
  );
}
```

---
## Authentication

For authentication, NextJS can integrate with libraries like [Clerk](https://clerk.com/docs/quickstarts/nextjs) or NextAuth.js. Common steps include:

- Wrapping your application or layout with an authentication provider.
- Using middleware (in `src/app/middleware.ts`) to protect routes.
- Leveraging server-side rendering for secure session management.

---

## App vs Page Routing

| Feature                | App Router                           | Page Router                                         |
| ---------------------- | ------------------------------------ | --------------------------------------------------- |
| File-based routing     | Uses nested folders to define routes | Files directly represent routes                     |
| Components             | Server Components by default         | Client Components by default                        |
| Data fetching          | fetch function for data fetching     | getServerSideProps, getStaticProps, getInitialProps |
| Layouts                | Layouts can be nested and dynamic    | Layouts are static                                  |
| Dynamic routes         | Supported, but syntax differs        | Supported                                           |
| Client-side navigation | Supported with router.push           | Supported with Link component                       |
| Priority               | Takes precedence over Page Router    | Fallback if no matching route in App Router         |

Page Router treats all files with`.js` and `.tsx` inside `/pages` directory as routes.
While App Router treats all directories with `/app` as routes.

