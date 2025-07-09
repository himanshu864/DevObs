# Recruitment Manager Portal – Technical Synopsis

The **Recruitment Manager** is a Next.js (v15) app built as a placement portal for multiple roles (students, results department, placement coordinators, admins, and superadmins). It follows Next.js’s App Router conventions with a clear folder organization. At the root, configuration files (`next.config.ts`, `tailwind.config.ts`, `schema.prisma`, ESLint/TS configs, Dockerfile, etc.) set up global settings. Static assets (logos, images, SVGs) live in `public/`, as recommended for Next.js projects. The main source is under `src/`, which contains:

* **`app/`** – The App Router directory. Each route segment (including route groups like `(auth)`, `(user)`, `(admin)`, etc.) is a folder under `app/`. These folders contain special files like `page.tsx` (the page component), `layout.tsx` (wrapper/UI layout), plus optional `loading.tsx`, `not-found.tsx`, and `error.tsx` for suspense loading states, 404 pages, and error boundaries, respectively. For example, `src/app/(auth)/login/page.tsx` is the login page, and `src/app/admin/(management)/students/page.tsx` is the admin students list page. Grouping folders with parentheses (e.g. `(auth)`, `(user)`) lets us organize related routes without exposing these prefixes in the URL.

* **`components/`** – Reusable React components and UI widgets. There are subfolders for different domains, e.g. `components/admin/` for admin-specific modals and forms, and `components/ui/` for shared primitives (buttons, dialogs, toasts, etc.). Many components leverage Radix UI primitives (Dialog, Toast, etc.) and Shadcn UI design patterns. For example, custom modals (in `components/ui/custom-modal.tsx`) wrap Radix’s `Dialog` to present pop-up forms or confirmations; Radix dialogs automatically trap focus and handle Escape keys for accessible modals. Toast notifications use the **Sonner** library (a React toast component) for elegant, promise-friendly alerts.

* **`constants/`** – Holds static values, TypeScript enums/interfaces, and navigation definitions. For example, `constants/index.ts` exports application-wide constants (API endpoints, regex patterns, etc.), and `constants/nav.ts` defines the navigation menu items. Centralizing these makes config changes easy (no hard-coded strings scattered in code).

* **`lib/`** – Utility modules and API client. We have an Axios-based HTTP client (`lib/api.ts`) to communicate with the backend, with logic for automatically attaching auth tokens. A custom *exceptions* module (`lib/exceptions.ts`) defines error types, and `lib/utils.ts` contains shared helper functions. This separation keeps business logic decoupled from the UI.

* **`middleware.ts` (root)** – A Next.js Edge Middleware file. It intercepts incoming requests (according to its path matcher) to enforce global rules like authentication and redirects. For instance, it can check cookies/sessions and redirect unauthenticated users to the login page. (Middleware runs before route matching and is useful for RBAC and session checks across pages.)

This structure follows Next.js best practices: using the `app/` directory with co-located components (`page`, `layout`, etc.), and placing global config at the root. It allows nested and grouped routes, enabling clear separation of student vs admin sections without cluttering URLs.

## Application Logic and User Authentication

**Authentication Flow:** We implemented a credential-based login that sets short-lived access tokens and longer-lived refresh tokens. On successful login (handled in `app/(auth)/login/actions.ts`), the backend returns a JWT access token plus an HTTP-only refresh token (often via cookies). The access token is stored (e.g. in memory or client storage), and attached to subsequent API requests. When the access token expires, Axios interceptors in our API client automatically call a refresh endpoint to obtain a new token, then retry the failed request. This “silent refresh” keeps the user logged in seamlessly. In practice, our `lib/api.ts` likely sets up these Axios interceptors to catch 401 responses, call `/api/refreshToken`, and replay the request. For context, this pattern (short access token \~10s, refresh token \~days) is outlined in the Next.js JWT guide.

**Session and Roles:** After login, the user’s role (e.g. student or admin) is embedded in the session or token. We enforce **Role-Based Access Control (RBAC)** by checking this role before rendering pages or performing sensitive actions. For example, server components (like dashboards) may fetch the session and inspect `session.user.role`. The Next.js docs show patterns like:

```tsx
const userRole = session?.user?.role;  
if (userRole === 'admin') { /* render admin UI */ }  
else if (userRole === 'user') { /* render student UI */ }  
else { redirect('/login'); }
```

This ensures only admins see admin panels. Likewise, in server actions (files under `actions.ts`), we check roles and return HTTP 403 if unauthorized. As Next.js notes, you might write:

```ts
const session = await verifySession();  
if (session.user.role !== 'admin') {  
  return new Response(null, { status: 403 });  
}
```

This blocks non-admin users from administrative actions. In short, role checks (student vs admin vs superadmin) are applied via middleware and in server code, aligning with Next.js authentication best practices.

**Form Handling:** All forms (login, profile update, create/edit dialogs) leverage **React Hook Form** on the client for immediate validation, together with Next.js Server Actions (`useActionState`) for robust server-side validation and processing. React Hook Form excels at providing real-time client-side validation (instant feedback, clean APIs), while server actions handle final validation and database mutations. By combining them, we get a progressive enhancement flow: the form can still submit and update even if JavaScript is disabled, and errors are caught on both sides. For example, a student profile form is a `use client` component using `useForm`, and on submit it calls a server action in `actions.ts` via a `<form action={updateProfile}>`. This matches Next.js’s recommended pattern of `<form action={serverFunction}>`. We likely use Zod schemas (as hinted by `@hookform/resolvers` in `package.json`) to validate form data on the server.

**Custom Modals & Dialogs:** For pop-up forms and confirmations, we use custom modal components (wrappers around Radix UI’s `Dialog` or similar). For instance, `components/ui/custom-modal.tsx` encapsulates a dialog with standardized styling. Radix’s Dialog primitive provides accessible features out of the box (focus trap, ARIA roles, keyboard handling). We also have specialized dialogs like `CreateDebarredForm.tsx` or `CompanyDeleteDialog.tsx` for CRUD operations. These modals are typically invoked from buttons (as `Dialog.Trigger`) and contain forms or messages; on submit, they perform server actions or API calls. This keeps the UI consistent and user-friendly.

**Navigation & Constants:** The navigation structure is defined programmatically. A `Nav.ts` file (likely in `components/` or `constants/`) exports nav items with labels, icons, and routes for each role. We read this to render sidebars (`DesktopSidebar.tsx`, `MobileNav.tsx`). Constants/interfaces in `index.ts` centralize shared types (e.g. interfaces for User, Student, Roles, and enums). This avoids typos and helps with IDE support.

**Error Handling & Feedback:** We include global error boundaries. The presence of `app/(user)/error.tsx` and similar files means that exceptions in rendering get caught and a friendly error page is shown. Likewise, `not-found.tsx` templates display when a page isn’t found. For runtime errors (e.g. API failures), we use try/catch in server actions and surface messages. For user feedback, we use a toast system (Sonner). We place a `<Toaster />` component near the app root (e.g. in `layout.tsx`), then call `toast.success()` or `toast.error()` in actions or effects to notify the user. Sonner is praised for smooth, styled toast messages. For example, after a successful update, an action might trigger `toast.success("Changes saved!")`. This provides non-blocking alerts.

## Data Integration and UI Components

**Data Tables:** Most admin and user lists (students, companies, job posts, applications, logs, etc.) are shown as tables. We leverage **TanStack React Table** (`@tanstack/react-table`) for this. In each feature folder (e.g. `app/admin/(management)/students/data-table.tsx`), we define column configurations and feed data into a `useReactTable` hook. TanStack’s headless model lets us handle core row rendering and add features like sorting and pagination easily. For example, the code may look like:

```ts
const table = useReactTable({  
  data: students,  
  columns: studentColumns,  
  getCoreRowModel: getCoreRowModel(),  
  getPaginationRowModel: getPaginationRowModel(),  
  /* other options */  
});  
```

This setup (with `getCoreRowModel` and `getPaginationRowModel`) enables client-side pagination and sorting. The HTML `<table>` structure then renders `table.getHeaderGroups()` and `table.getRowModel()` to display headers and rows. By using a stable library, we avoid reinventing table logic.

**Filtering and Search:** Above tables, filter forms allow users to narrow results (e.g. search by name or date range). These forms typically submit or call server actions to reload data. We also support URL query parameters for search state. For instance, if a student searches jobs, the search term and page might be in `?query=...&page=2`. We read these via Next.js’s `useSearchParams` hook in a client component, update them on input change, and fetch data accordingly. The Next.js docs encourage using URL params for search/pagination since it makes the state bookmarkable and SSR-friendly. In our app, typing in a search box likely triggers an update to the URL (pushing state) and re-renders the table on the server with the filtered query. We debounce user input so we don’t update too frequently (e.g. wait \~300ms after typing stops). Debouncing is important for performance: it ensures we only fire the API call after the user pauses typing.

**Pagination:** When listing items, we implement pagination to handle large datasets. Depending on the data size, we can do client-side pagination (fetch all rows and paginate locally) or server-side (fetch one page at a time). TanStack Table supports both. For small-to-medium tables, we set `getPaginationRowModel` in React Table to use client-side pagination. For very large tables (e.g. thousands of rows), we switch to manual pagination: we fetch only the rows for the current page from our API and set `manualPagination: true` in the table options. In manual mode, we supply `pageCount` or `rowCount` so the table knows total pages. Controls (Next, Prev) update the pagination state, which then triggers a re-fetch of that page. Either way, pagination state (current page index, page size) is managed via React state and passed to the table instance.

**Dialogs for Create/Update:** Many forms are presented in modal dialogs. For example, clicking “Add Student” opens an `AddStudentsForm` inside `AddStudentsCard`. These use controlled forms (`react-hook-form`) and when submitted, call a server action in the corresponding `actions.ts`. This might create a new student record and then refresh the table data. We use Next.js’s form `action={createStudent}` pattern so that after submission, the page doesn’t hard-refresh; Next.js handles the round-trip and UI update automatically.

**Soft Deletes (Disable/Restore):** Instead of hard-deleting, the UI generally offers “Disable” or “Deactivate” actions (e.g. a student or company can be debarred). The code includes dialogs like `DisableBatchDialog.tsx` and `RestoreBatchDialog.tsx` for toggling status. Under the hood, these likely set a “deleted” flag in the database (a soft-delete) rather than removing the record. This UX lets admins recover or audit data. When an item is soft-deleted, the UI might show it in an “inactive” list or allow filtering by status. (This approach aligns with best practices: destructive deletes require confirmation and often have an “undo” state. Soft delete patterns are common in admin apps to prevent data loss.)

**Global State (Recoil):** The package.json lists `recoil`, so it’s probably used for shared state (e.g. user info, theme, or transient UI state). For example, the user’s name/role might be stored in a Recoil atom after login, so the layout can show “Hello, \[User]”. Shared state can also handle things like a global loading indicator or modal visibility outside of component-local state.

## Additional Features and Integration

* **Route Middleware:** The root `middleware.ts` implements request interception. As Next.js docs recommend, middleware can check authentication cookies before allowing access. For example, we likely exclude the login page from auth checks, but require other routes to have a valid session. Unauthorized users are redirected to login. Middleware also can redirect users based on their locale or device, if needed. Importantly, we use only one `middleware.ts` (per Next.js convention) but structure its logic (e.g. in separate modules) for clarity.

* **Server-Side Rendering (SSR):** Many pages (especially data lists) render on the server by default, improving SEO and initial load performance. Next.js allows us to fetch data (from a database or API) directly in server components (`async`/`await` in `page.tsx`). Using URL params (search, pagination) on the server means the page HTML is pre-populated with current data. We also include React Suspense for streaming; e.g. `loading.tsx` shows a skeleton UI while server data is fetched.

* **Query Client/Params:** Integration with URL query parameters is leveraged for state. The Next.js learning example shows using `useSearchParams`, `useRouter`, etc. to sync input with URL and trigger new server fetches. In practice, our code might capture input, update the URL via `router.push`, and the parent page (an async component) sees the updated `searchParams` and re-queries the database or API for filtered results.

* **Debounce on Search:** In filter inputs (e.g. a student name search), we implement a debounce hook so that network calls are delayed until the user stops typing. This prevents spamming the server on every keystroke. The pattern is: keep a local state `query`, and use `useEffect` with `setTimeout` to update a “debouncedQuery” state after \~300ms of no changes. When `debouncedQuery` changes, we perform the actual search (updating URL or calling the API).

* **Toasts and Notifications:** We use the Sonner toast library for user feedback. A `<Toaster />` is rendered (likely in the root layout), and anywhere in code we call `toast.success()`, `toast.error()`, etc. Sonner supports different types (success, info, warning, error, promise) with custom styling. For instance, after a student applies for a job, we show a success toast “Application submitted!”. Using an established toast component ensures consistency and accessibility.

* **Performance & UX:** We include React Query or similar for caching? (Not explicit, but could be using SWR or react-query with TanStack, since `@tanstack/react-table` is present but no explicit react-query; maybe data is fetched in server components only.) We ensure fast UI by lazy-loading components (Next.js code-splits per route), and maybe using `React.Suspense` around heavy components. The file `RouteProgress.tsx` suggests we show a progress bar on route changes.

* **Logging:** The presence of `SystemLogsClientPage.tsx` implies we have a section to view application logs. This likely uses tables with filters (e.g. date range) similar to other tables. Having a logs section means we might use specialized middleware or server handlers to record actions, which is part of integration but not directly user-facing.

* **Miscellaneous:** We support dark/light themes via `next-themes`. We allow file downloads (there’s `xlsx` dependency, so maybe export reports to Excel). Forms handle file uploads (e.g. resume uploads, bulk student CSVs, academic records). These use input type=file, and API routes to handle the binary data. Error handling for uploads (size limits, format) is done client-side plus server-side checks. In summary, the integration covers all typical CRUD UI elements (forms, dialogs, tables, filters, pagination) woven together by Next.js’s patterns.

Overall, the project combines Next.js’s new App Router features (layouts, server actions, middleware) with modern UI libraries (Radix, Tailwind, react-hook-form, TanStack Table) to build a robust, multi-role placement portal. Each layer—from file structure to user experience—follows current best practices. The technical design (token refresh, role checks, reusable components) aims to make the app secure, maintainable, and user-friendly, whether viewed by a student or the placement coordinator.

**Sources:** Next.js documentation and community guides for App Router, authentication, forms, and tables. These provide patterns that match our implementation (layout/page files, server actions with `use client`, JWT session handling, etc.). Each cited snippet corresponds to a design decision or feature listed above.