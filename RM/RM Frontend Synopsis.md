# Why Resume Manager?

## Introduction

In the ever-evolving landscape of campus recruitment and placement processes, institutions face significant challenges in managing student profiles, coordinating with companies, and maintaining data integrity. The original placement management system, developed in PHP on fragile physical servers, struggled to accommodate the growing needs of the Training and Placement Department. It exhibited severe scalability issues, insecure deployment practices, and an inflexible permission model that hampered efficient operations. To address these shortcomings and future-proof our infrastructure, the decision was made to develop **Resume Manager (RM)**: a modern, secure, and scalable platform leveraging cutting-edge web technologies.

## Shortcomings of the Previous System

1. **Monolithic PHP Architecture**  
    The legacy system was built entirely in PHP with tightly coupled modules. Any change in one component often triggered unexpected issues in others, leading to long integration cycles and unpredictable downtime.
    
2. **Scalability Constraints**  
    Hosted on on-premises physical servers, the application could not scale elastically to handle peak recruitment seasons. Slow response times and frequent service degradation became commonplace as user load increased.
    
3. **Data Migration Headaches**  
    Bulk operations, such as importing new student batches and academic records, relied on ad hoc scripts prone to data loss and format inconsistencies. The process was manual, slow, and error-prone.
    
4. **Insecure Deployment Practices**  
    Without standardized CI/CD pipelines or containerization, deployments were executed by hand, introducing configuration drift and security vulnerabilities. Sensitive credentials were hard-coded or stored insecurely.
    
5. **Rigid Permission Model**  
    The system supported only fixed permission sets. As departmental roles evolved, administrators had to request code changes to modify access, resulting in slow turnaround times and potential misalignments with organizational needs.
    
6. **Prone to Scams and Tampering**  
    Inadequate logging and weak data validation opened the door to fraudulent activities. Companies and students alike reported instances of unauthorized access and tampering with application records.
    
7. **Cumbersome Bulk Operations**  
    Uploading large Excel files and executing bulk data transformations often led to timeouts and incomplete imports. Students and administrators were left waiting for hours to reconcile records.
    

## Vision and Improvement Goals

To overcome these deficiencies, RM was conceived with the following objectives:

1. **Modular, Scalable Architecture**  
    Adopt a microservices-inspired structure to isolate concerns, allowing independent scaling of frontend, backend, and batch-processing services.
    
2. **Modern Tech Stack**  
    Leverage Next.js, TypeScript, and Tailwind CSS on the frontend; introduce robust validation with Zod; and automate deployments with containerization (Docker) and CI/CD pipelines.
    
3. **Flexible, Role-Based Access Control**  
    Implement a dynamic RBAC system with customizable CRUD permissions for Superadmin, Admin, PC, Result, and Student roles—enabling on-the-fly adjustments without code changes.
    
4. **Secure, Automated Deployments**  
    Establish a standardized pipeline for builds, tests, and deployments to cloud environments, ensuring consistent configuration and minimizing human error.
    
5. **Efficient Bulk Data Handling**  
    Create background jobs and server-side parsers for Excel imports, with real-time progress tracking and error reporting—transforming an overnight task into an automated, reliable workflow.
    
6. **End-to-End Traceability**  
    Capture comprehensive logs of all actions (file uploads, data modifications, system events) to provide an audit trail that prevents tampering and supports compliance.
    
7. **Enhanced UI/UX**  
    Design an intuitive frontend with responsive tables, advanced filtering, and actionable notifications—reducing user friction and accelerating student and administrator workflows.
    

## Initial Challenges

1. **Designing a Scalable Architecture**  
    Crafting a loosely coupled system demanded careful planning of API boundaries, state management, and data synchronization. We evaluated multiple architectural patterns before settling on a hybrid SSR/CSR model powered by Next.js.
    
2. **Stakeholder Alignment**  
    Balancing the requirements of the Training and Placement Department, institutional IT, and end-users required iterative workshops and feedback sessions. Misalignments in priorities surfaced early and were resolved through a shared product roadmap.
    
3. **Data Migration Complexity**  
    Converting decades of student records from heterogeneous legacy formats into a unified schema posed data-cleaning and validation challenges. We developed transformation scripts with rollback capabilities to mitigate risks during trial runs.
    
4. **Establishing DevOps Practices**  
    Introducing CI/CD, container orchestration, and automated testing into an environment accustomed to manual workflows called for training sessions and documentation. The team initially grappled with Docker networking and cloud provisioning nuances.
    
5. **Implementing Robust RBAC**  
    Building a permission engine that could dynamically grant or revoke granular access required defining a comprehensive set of resource-action pairs and designing an intuitive admin UI for policy management.
    

## Team Formation and Collaboration

To tackle these multifaceted challenges, we assembled a cross-functional team:

- **Frontend Leads (2)**  
    Focused on crafting reusable React components, state management with React Query, and implementing design tokens via Tailwind CSS.
    
- **Backend Leads (2)**  
    Handled API design, database schema evolution, background job orchestration, and integration of Excel parsing libraries.
    
- **Extended Frontend Cohort**  
    As scope expanded, we onboarded three senior developers and nine juniors under a dedicated Frontend Head—facilitating faster feature delivery and mentoring.
    
- **Backend Head & Integration Lead**  
    Oversaw overall system architecture, coordinated between teams, and managed deployment pipelines in Docker and Kubernetes.
    
- **Single Supervisor**  
    Appointed to ensure cohesion, track progress, and maintain our development roadmap—empowering individual teams while preserving alignment.
    

Each member had clear responsibilities, and we instituted weekly sprint reviews, daily stand-ups, and bi-weekly demos. This structure fostered accountability, knowledge sharing, and rapid iteration—laying the groundwork for RM’s successful launch.

---
# Tech Stack

In designing Resume Manager (RM), we selected a modern, cohesive tech stack tailored to our project goals: performance, scalability, developer productivity, and maintainability. Below is an in-depth discussion of each core technology, alternatives we considered, and our rationale for final choices.

## Next.js (v15.2.4)

### Rationale for Choosing Next.js

1. **Server-Side Rendering (SSR) & Static Generation**  
    Next.js seamlessly blends server-side rendering with static-site generation (SSG), giving us performance benefits and SEO friendliness out-of-the-box. During peak application traffic—particularly during mass placement seasons—pre-rendered pages and incremental static regeneration (ISR) ensure consistently fast response times and reduced server load.
    
2. **File-Based Routing**  
    Built-in file-based routing in Next.js dramatically accelerates development. Creating a new page only requires adding a file under the `pages/` or `app/` directory, automatically mapping URLs to components without boilerplate route definitions.
    
3. **API Routes & Middleware**  
    Next.js API routes allow us to define backend endpoints alongside frontend code, simplifying project structure and deployment. Its middleware layer supports granular request handling (e.g., authentication, logging) at the edge.
    
4. **Incremental Adoption & Familiar React Ecosystem**  
    Our team’s existing expertise in React made the learning curve for Next.js minimal. We could incrementally adopt advanced Next.js features (e.g., `app/` directory, `getServerSideProps`) while still writing familiar React components.
    
5. **Built-In Performance Optimizations**  
    Next.js includes image optimization, code splitting, and fast refresh, contributing to a snappy developer experience and optimized production bundles.
    

### Alternatives Evaluated

- **Create React App (CRA)**: Lacks SSR/SSG, built-in routing, and API routes. Would require additional configuration (e.g., React Router, Express) and inevitably introduce more maintenance overhead.
    
- **Gatsby**: Excellent for static sites, but its GraphQL data layer and build times did not align with our dynamic, user-driven application needs.
    
- **Angular**: A full-fledged framework with dependency injection and opinionated architecture. However, the steep learning curve and complexity of setting up SSR with Angular Universal led us to favor Next.js’s lightweight DX.
    
- **Remix**: While promising, Remix’s community and plugin ecosystem were less mature at the time of project kickoff.
    

## TypeScript (v5)

### Benefits

1. **Static Typing for Reliability**  
    TypeScript’s type system catches errors at compile time, reducing runtime bugs and improving refactor safety—crucial for a large codebase with multiple contributors.
    
2. **Autocompletion & Developer Experience**  
    IDE integrations enable intelligent code completion, easier navigation, and inline documentation, accelerating development velocity.
    
3. **Interface Contracts Between Frontend and Backend**  
    We defined shared types (e.g., `StudentProfile`, `ApplicationStatus`) used by both the frontend and backend, enforcing consistency and preventing schema drift.
    

### Alternatives

- **JavaScript (ES6+)**: Faster to start, but prone to type-related bugs in complex flows. Lacked the safety net TypeScript provides.
    
- **Flow**: Similar static typing, but with a smaller community and less integration with Next.js.
    

## ShadCN/UI

### Why ShadCN

1. **Headless Component Library**  
    ShadCN/UI provides unstyled, accessible components (dialogs, dropdowns, tables) that integrate perfectly with Tailwind CSS utility classes, allowing us to implement a minimalistic design system without overriding opinionated styles.
    
2. **Customizability & Theming**  
    Components can be themed via Tailwind tokens, giving us full control over visuals. We standardized our design language—typography, spacing, colors—through a shared Tailwind config and ShadCN components.
    
3. **Seamless Next.js Compatibility**  
    ShadCN/UI’s architecture aligns with Next.js conventions (e.g., tree-shakeable imports), minimizing bundle size.
    

### Alternatives

- **Chakra UI**: Rich component set but comes with default styling that often needs overriding, increasing bundle size and CSS specificity issues.
    
- **Material-UI (MUI)**: Heavier footprint and more “Google Material” aesthetic than our clean, minimal vision.
    
- **Tailwind UI**: Excellent designs, but requires a paid license and doesn’t offer the same level of code-based customization as ShadCN.
    

## Tailwind CSS (v3.4.17)

### Advantages

1. **Utility-First Approach**  
    Tailwind’s atomic classes enable rapid prototyping and consistent spacing, sizing, and typography without writing custom CSS.
    
2. **Responsive & Dark Mode Utilities**  
    Built-in responsive prefixes (`sm:`, `md:`) and dark-mode support (`dark:`) simplified theme toggling and mobile-first design.
    
3. **JIT Compilation**  
    The Just-In-Time engine generates only the classes we use, keeping CSS bundle sizes minimal and rebuild times fast.
    

### Alternatives

- **Bootstrap**: Provides a pre-styled framework but is opinionated and less flexible for our custom design tokens.
    
- **CSS Modules / SCSS**: Modular CSS approach, but with higher maintenance overhead and less agility for iterative UI tweaks.
    

## Zod (v3.25.67) & React Hook Form Integration

### Role in RM

1. **Schema Validation**  
    Zod defines schemas for API payloads (e.g., student registration, job post creation). We validate data on both client and server, ensuring end-to-end contract verification.
    
2. **Type Inference**  
    Zod-derived types automatically flow into TypeScript interfaces, reducing duplication and guaranteeing consistent types.
    
3. **React Hook Form Resolver**  
    By combining Zod with React Hook Form (`@hookform/resolvers`), form state management, validation, and error messaging are unified, yielding concise form components.
    

### Alternatives

- **Yup**: Mature library but lacks TypeScript-first design and type inference quality of Zod.
    
- **io-ts**: Powerful codec-based validation, but more verbose and complex to set up.
    

## Sonner (Toaster Notifications)

### Why Sonner

1. **Declarative Toast API**  
    Simple APIs (`toast.success('...')`, `toast.error('...')`) integrate easily into async flows (API calls, form submissions).
    
2. **Customizable UI**  
    We styled Sonner’s toasts using Tailwind classes to match our design system, ensuring consistency across notifications.
    
3. **Lightweight**  
    Minimal footprint and no external dependencies beyond React.
    

### Alternative

- **React-Toastify**: Feature-rich but heavier and with a less flexible theming model.
    

## date-fns (v3.0.0)

### Use Cases

1. **Formatting & Parsing Dates**  
    Consistent display of dates (e.g., application deadlines, interview schedules) in various locales.
    
2. **Immutable API**  
    Functions return new Date instances without side effects, simplifying state management.
    
3. **Tree-Shakable Modules**  
    We import only the functions we need (`format`, `parseISO`), keeping bundle sizes optimized.
    

### Alternatives

- **Moment.js**: Deprecated status, large bundle, mutable API.
    
- **Luxon**: Modern and powerful, but larger than date-fns and with fewer community plugins.
    

## ESLint & Prettier

### ESLint (v9)

1. **Static Code Analysis**  
    Custom rules (via `eslint-config-next` and `eslint-plugin-prettier`) catch potential bugs, anti-patterns, and stylistic issues before merging.
    
2. **Team Enforced Standards**  
    Shared config ensures all contributors adhere to the same code quality guidelines.
    

### Prettier (v3.5.3) & `prettier-plugin-tailwindcss`

1. **Automated Formatting**  
    Prettier’s opinionated formatting eliminates style debates. Combined with `prettier-plugin-tailwindcss`, class lists are sorted and grouped logically.
    
2. **CI Integration**  
    `npm run format` and `npm run lint` are enforced in pre-commit hooks, maintaining a clean codebase.
    

## Lucide-React (v0.485.0)

1. **Minimal and Consistent Icons**  
    Lucide icons are simple, outline-based SVGs that align with our minimal UI ethos.
    
2. **Tree-Shakable Imports**  
    We import individual icon components only where needed, preventing unnecessary bloat.
    
3. **Accessibility**  
    Lucide provides built-in `aria-hidden` defaults and supports accessible titles.
    

### Alternative

- **React-Icons**: Broad icon support, but sometimes inconsistent style across icon packs.
    
- **Heroicons**: Tightly coupled to Tailwind Labs; less extensive library than Lucide.
    

## Additional Tooling

- **clsx & tailwind-merge**  
    Simplify conditional className concatenation and handle utility conflicts gracefully.
    
- **cmdk & Radix UI**  
    For building custom command palettes, dropdowns, and accessible primitives without wrestling with styling opinionated components.
    
- **Docker & CI/CD**  
    Containerized development environments and automated pipelines (GitHub Actions) for linting, testing, and deployments to ensure consistency across local, staging, and production.
    

### Summary

Our chosen stack strikes a balance between developer productivity and application performance. By leveraging Next.js’s hybrid rendering model, TypeScript’s safety, Tailwind’s agility, and a suite of headless, lightweight UI and utility libraries, we delivered a modern placement platform. Each dependency was scrutinized against alternatives to guarantee alignment with RM’s objectives: a scalable, secure, maintainable, and performant experience for students, administrators, and companies alike.

---
# Application Logic

Resume Manager’s frontend logic is engineered to deliver a seamless, maintainable, and scalable experience. Our Next.js codebase spans over 4,500 lines of TypeScript, organized into clear patterns covering file structure, API abstraction, error/loading states, authentication, form handling, custom components, and state management. This chapter delves into each aspect, reflecting industry best practices and our own enhancements.

## 1. Folder & File Structure

A coherent structure promotes discoverability and consistency. We follow Next.js conventions while introducing domain-driven groupings:

```
src/
├── app/               # Next.js `app` directory: each subfolder is a route segment
│   ├── (auth)/        # Auth flow: layout.tsx & login page
│   ├── (share)/       # Public shareable applications module
│   ├── (user)/        # Student-facing routes (dashboard, applications, profile)
│   ├── admin/         # Admin portal: nested management modules (academics, jobposts, RBAC)
│   ├── api/           # Edge API routes (my-resumes, withdraw)
│   ├── layout.tsx     # Global layout: nav, toasters, footers
│   ├── loading.tsx    # Route-level Suspense fallback UI
│   ├── not-found.tsx  # Custom 404 page
│   └── page.tsx       # Landing page (SSR)

src/
├── components/        # Reusable UI components
│   ├── ui/            # Headless primitives: Button, Dialog, Table
│   ├── admin/         # Admin-specific components: DataTable, Forms, Modals
│   └── user/          # Student components: JobCard, ResumeUpload, Notifications

src/
├── constants/         # Shared constants & enums
│   ├── index.ts       # TS interfaces & enums (Role, ApplicationStatus)
│   └── nav.ts         # Sidebar item definitions with role guards

src/
├── lib/               # Core logic & utilities
│   ├── api.ts         # `fetchApi` wrapper with retry & interceptor logic
│   ├── exceptions.ts  # Custom Error classes: ApiError, ValidationError
│   └── utils.ts       # `formatDate`, `debounce`, `serializeQuery`

src/
└── middleware.ts      # Global auth guard, role-based redirects, logging
```

Key benefits:

- **Separation of concerns**: Routes, UI, constants, and logic are distinct.
    
- **Scalability**: New features map directly into folders.
    
- **Onboarding**: Developers quickly locate relevant code.
    

## 2. API Abstraction & Error Handling

### 2.1 Custom `fetchApi` Utility

Rather than introducing Axios, we crafted a lightweight `fetchApi` in `lib/api.ts`:

- **Base Configuration**: `BASE_URL`, JSON headers, credentials inclusion (cookies).
    
- **Interceptors**: Pre-request hook attaches access tokens; post-response hook handles status codes.
    
- **Retry Logic**: Automatic retry on HTTP 502, 503, and timeouts, with exponential backoff.
    

```ts
// lib/api.ts
export async function fetchApi<T>(
  path: string,
  options: RequestInit = {}
): Promise<T> {
  const res = await fetch(`${BASE_URL}${path}`, {
    ...options,
    headers: { 'Content-Type': 'application/json', ...options.headers },
    credentials: 'include',
    signal: timeoutSignal(10_000)
  });

  if (!res.ok) {
    const payload = await res.json();
    throw new ApiError(res.status, payload.message || res.statusText);
  }

  return res.json();
}
```

### 2.2 Error Handling Patterns

- **Custom Error Classes**: `ApiError` and `ValidationError` distinguish between network and schema issues.
    
- **Global Error Boundaries**: Each route defines `error.tsx`, catching render-time errors and displaying fallback UIs plus toast notifications.
    
- **Centralized Logging**: Errors are reported to a remote logging service (e.g., Sentry) inside the error boundary.
    

```tsx
// app/(user)/error.tsx
'use client';
import { toast } from 'sonner';

export default function UserError({ error }: { error: Error }) {
  toast.error(error.message);
  logErrorToService(error);
  return <ErrorDisplay message={error.message} />;
}
```

Benefits:

- **User Feedback**: Immediate toaster alerts.
    
- **Maintainability**: Consistent error UI across routes.
    
- **Observability**: Central logs allow post-mortem debugging.
    

## 3. Loading & Not Found States

### 3.1 Suspense Loading

Next.js 13’s `loading.tsx` supports route-level Suspense:

```tsx
// app/loading.tsx
export default function Loading() {
  return <SkeletonPage />; // custom skeleton placeholders
}
```

- Skeletons for tables, cards, and forms use ShadCN `Skeleton` components.
    
- Avoids Flash of Unstyled Content (FOUC) and improves perceived performance.
    

### 3.2 Not Found Handling

`not-found.tsx` is rendered when a page’s data fetch returns 404:

```tsx
// app/not-found.tsx
export default function NotFound() {
  return (
    <div className="text-center py-20">
      <h1 className="text-4xl">Page Not Found</h1>
      <p>Sorry, we couldn’t locate that resource.</p>
      <Link href="/">Go Home</Link>
    </div>
  );
}
```

This flow frees developers from manual try/catch blocks, relying on framework conventions.

## 4. Toaster Notifications

A single `Toaster` instance is placed in the root `layout.tsx`:

```tsx
// app/layout.tsx
import { Toaster } from 'sonner';
export default function RootLayout({ children }) {
  return (
    <html>
      <body>
        {children}
        <Toaster position="bottom-right" />
      </body>
    </html>
  );
}
```

Toasts are invoked from anywhere:

```ts
// example in an async action
try {
  await fetchApi('/jobposts', { method: 'POST', body: JSON.stringify(data) });
  toast.success('Job post created');
} catch (err) {
  toast.error(`Error: ${err.message}`);
}
```

Benefits:

- **Global Feedback Mechanism**: Uniform messaging across modules.
    
- **Asynchronous Flow Handling**: Supports loading toasts and promise chaining.
    

## 5. Authentication & Authorization

### 5.1 Token Lifecycle

- **Access Token**: JWT stored in HTTP-only cookie, 15-minute validity.
    
- **Refresh Token**: HTTP-only cookie, 1-hour validity.
    
- **Middleware** (`middleware.ts`) intercepts requests to:
    
    1. Validate access token.
        
    2. Attempt refresh if expired.
        
    3. Redirect to `/login` on failure.
        

### 5.2 Role-Based Route Guards

Using Next.js Middleware and route matchers:

```ts
// middleware.ts
export function middleware(req) {
  const { role } = verifyJwt(req.cookies.get('accessToken'));
  if (req.nextUrl.pathname.startsWith('/admin') && !roleAllowsAdmin(role)) {
    return NextResponse.redirect('/forbidden');
  }
  // similar logic for student routes
  return NextResponse.next();
}
```

This edge-layer enforcement ensures frontend pages are never delivered to unauthorized users.

## 6. Form Handling & Validation

We standardize forms with **React Hook Form** and **Zod**:

```ts
// components/admin/CreateJobPostForm.tsx
const jobSchema = z.object({
  title: z.string().min(5),
  description: z.string().min(20),
  deadline: z.string().refine(isValidISODate, 'Invalid date'),
});

export function CreateJobPostForm() {
  const form = useForm({ resolver: zodResolver(jobSchema) });
  const onSubmit = form.handleSubmit(async (values) => {
    await fetchApi('/jobposts', { method: 'POST', body: JSON.stringify(values) });
    toast.success('Created successfully');
  });

  return (
    <form onSubmit={onSubmit}>
      <Input label="Title" {...form.register('title')} />
      <Textarea label="Description" {...form.register('description')} />
      <Input type="date" {...form.register('deadline')} />
      <Button type="submit" disabled={form.formState.isSubmitting}>
        Submit
      </Button>
    </form>
  );
}
```

Advantages:

- **Unified Validation**: Client and server both reference the same Zod schemas.
    
- **Developer Ergonomics**: `useForm` hooks streamline state management and error handling.
    
- **Edge-Case Coverage**: Schema refinements catch malformed input before API calls.
    

## 7. Custom Modals & Dialogs

Building on Radix UI and ShadCN styles, our `CustomModal` supports:

- **Dynamic Content**: Pass any React node as body.
    
- **Action Slots**: Header, content, footer slots for buttons.
    
- **Accessibility**: Focus trap, ARIA labels, keyboard navigation.
    

```tsx
// components/ui/custom-modal.tsx
export function CustomModal({
  trigger, title, children, footer
}: ModalProps) {
  return (
    <Dialog>
      <DialogTrigger asChild>{trigger}</DialogTrigger>
      <DialogContent>
        <DialogHeader><h2>{title}</h2></DialogHeader>
        <DialogBody>{children}</DialogBody>
        <DialogFooter>{footer}</DialogFooter>
      </DialogContent>
    </Dialog>
  );
}
```

Used extensively in admin flows: editing students, confirming bulk debarment, exporting records, etc.

## 8. Data Fetching & Component Patterns

### 8.1 Server vs. Client Components

- **Server Components**: Default in `page.tsx`, fetch data directly via `fetchApi`, free of client-side bundle.
    
- **Client Components** (`'use client'`): For interactive parts—debounced search inputs, real-time toast handling.
    

This split reduces bundle size and exploits React Server Components for performance.

### 8.2 Standardized Table Module

To maintain consistency, each admin feature (e.g., `jobposts`, `students`) follows a four-file pattern in its directory:

1. **`columns.tsx`**: Defines column schemas, cell renderers, sort keys.
    
2. **`data-table.tsx`**: Wraps `<Table>` with TanStack React Table hooks for pagination, sorting, filtering.
    
3. **`actions.ts`**: Row-level operations—edit, delete, share—using `fetchApi`.
    
4. **`page.tsx`**: Server-rendered page that fetches initial data and renders `<DataTable>`.
    

Example: `src/app/admin/(management)/jobposts`

Benefits:

- **Uniform UX**: Tables behave identically across modules.
    
- **Ease of Extension**: New entity tables adopt the same files.
    
- **Reduced Cognitive Load**: Developers reuse patterns instead of inventing per feature.
    

## 9. Navigation & Constants

Central files in `src/constants`:

- **`index.ts`**: Interfaces (`User`, `Company`, `Application`), enums (`Role`, `LogType`).
    
- **`nav.ts`**: An array of navigation items:
    
    ```ts
    export const navItems = [
      { label: 'Dashboard', icon: HomeIcon, path: '/dashboard', roles: ['student','admin'] },
      // …
    ];
    ```
    

Sidebars and mobile menus import `navItems` and filter by the current `user.role`, ensuring only authorized links appear.

## 10. Utility Library

`src/lib/utils.ts` consolidates pure functions:

- **`formatDate(date: string): string`**: Uses `date-fns` to render `dd MMM yyyy`.
    
- **`debounce(fn, wait)`**: Generic debounce for input handlers, preventing API spamming.
    
- **`serializeQuery(params: Record<string, any>): string`**: URL-encodes filter objects into query strings for pagination and filtering.
    

By centralizing these, we avoid duplication and ensure consistent behavior.

# Industry Practices Reflected

1. **Convention over Configuration**: Folder conventions and standardized file patterns reduce decision fatigue.
2. **Infrastructure as Code**: Dockerfiles, CI YAML, and Terraform (for backend) ensure environment parity.
3. **Shift-Left Testing**: Unit tests for utilities, integration tests for critical flows, and E2E tests (Playwright) guard regressions.
4. **Accessibility**: All interactive elements (forms, modals, tables) follow WCAG guidelines using Radix primitives.
5. **Performance Monitoring**: Real user metrics (Web Vitals) tracked via analytics and Lighthouse CI.
6. **Security Best Practices**: HTTP-only cookies, CSRF protection, Content Security Policies, Role-based route guarding at edge.
7. **Documentation & Onboarding**: In-repo `README.md`, `docs/` folder with architecture diagrams, and an internal dev wiki.

## Conclusion

The Application Logic layer of Resume Manager embodies a mature front-end architecture—balancing Next.js innovations (server components, file routing) with proven React best practices (custom hooks, headless UI). Consistent patterns in file structure, API handling, forms, and tables streamline development and maintenance. This foundation empowers our expanding team to deliver features rapidly, safely, and reliably as RM scales to serve thousands of students and companies.

Great! I’ll now write a comprehensive Integration chapter (~6,000–7,000 words), detailing forms, tables, filters, pagination, modals, soft-deletes, optimization patterns, and reusable components—along with the design philosophy behind them. I’ll include relevant code patterns, use case examples, and consistent formatting as with previous sections. I’ll let you know as soon as it’s ready for your review.

---
# Integration

In modern web apps, consistent patterns for forms, tables, filtering, and navigation greatly improve developer productivity and user experience. We invested heavily in **reusable components and patterns** so that new data-driven pages can be built with minimal boilerplate. By standardizing how forms, tables, modals, filters, and pagination work, each new route merely configures a few pieces (schema, columns, API calls) but relies on a proven structure. Below we walk through each feature in depth, explaining both the implementation and the underlying rationale.

## Efficient Form Handling with `useActionState`

For interactive forms (create/edit), we use React 19’s [`useActionState`](https://react.dev/reference/react/useActionState) hook. This hook ties a server action’s result to component state so that submitting a form immediately updates the UI with the response. In practice, we define server-side action functions (e.g. in `actions.ts`) for creating or updating records. In the client component we call:

```jsx
const [result, formAction, isPending] = useActionState(createRecord, null);
```

The `formAction` is passed as the form’s `action` prop (or as `formAction` on a submit button). When submitted, the server action runs and its return value becomes `result`. We can show errors or confirmation messages based on this state. Notably, **with server actions**, React will even render the server’s response _before_ full hydration. The `isPending` flag tells us when a request is in flight, so we can disable inputs or show spinners.

In some cases we invoke the form action manually. For example, clicking a button outside a `<form>` can trigger the same action by wrapping it in `startTransition`. As one React contributor explained: “You can call an action outside a form but it must be inside `startTransition`”. We implement:

```tsx
<button
  type="button"
  onClick={() => startTransition(() => formAction(formData))}
>
  Submit
</button>
```

Here, `startTransition(() => formAction(data))` dispatches the action as a non-blocking transition. This pattern simplifies code: errors and loading states are managed by the hook, so we avoid manual state tracking. Using `useActionState` also consolidates _before_ and _after_ states. For example, if the action returns validation errors, we can set the initial state accordingly and display them in the form. Overall, forms become reactive and simple: define the server logic once, hook it up with `useActionState`, and let the framework propagate results to the UI. This approach drastically cuts boilerplate compared to manually wiring up React state and effects.

## Custom Data Tables with Shadcn UI

We built a **reusable data table component** by combining TanStack Table (a headless table library) with Shadcn UI’s styled `<Table>` components. The Shadcn [Data Table guide](https://ui.shadcn.com/docs/components/data-table) shows this pattern: “use TanStack Table and the `<Table />` component to build your own custom data table”. In practice, each feature page defines a `columns.tsx` that exports `ColumnDef<T>[]` describing the data fields, headers, and cell renderers. We then use a generic `<DataTable>` component (a client component) that takes data and columns as props.

Within `<DataTable>`, we set up the TanStack table instance, render headers and rows with Shadcn’s `<TableHeader>`, `<TableRow>`, `<TableCell>`, etc. This allows flexible features: **sorting, filtering, hiding columns, and row selection**. We also insert action buttons or menus into cells. For example, one column might render “Edit” and “Delete” buttons (often opening a modal or invoking `useActionState`). Another column may have a dropdown menu per row. These interactive elements are standard inside our `<DataTable>`, so every table has consistent UX. We also include a toolbar above or below the table for selected-row count and pagination controls (see below).

Because this table logic is encapsulated, adding a new table page is mostly about providing columns and data. For example, a “Users” page might supply columns for name, email, role, plus a “Status” badge cell. The `<DataTable>` then handles rendering, pagination buttons, and selection. We also include an optional “column visibility” menu (checkboxes to hide/show columns) by default, enabling end-users to customize the table view.

**Key points:**

- Tables use a consistent structure (header groups, rows, cells) following Shadcn’s pattern.
- Action controls (buttons, dropdowns) are embedded in table cells for direct operations.
- We support client-driven sorting or server-driven sorting: since we fetch data server-side, many tables simply render sorted/filt ered data as-is.
- A reusable pagination component (see next section) lives below the table.

## Filtering with Forms and Query Parameters

To let users filter data, we implemented a **filter panel** (often a Shadcn “Sheet” or sliding dialog) containing a form. This form uses Zod schemas for validation and defines fields corresponding to query parameters. For instance, a “Status” dropdown might use a Zod `enum` to validate allowed values, and a “Date from/to” would use a Zod `date()` schema. Using Zod ensures that only valid query values are used on the server (guards against injection or bad input).

When the user submits the filter form, we serialize the input into URL search parameters. In Next.js App Router, we typically call something like `router.replace(\`${pathname}?${params.toString()}`)`to update the URL without a full reload. This means the page’s`searchParams`prop (or`useSearchParams` hook in client components) is updated, and our server component fetching data sees the new params. As the official tutorial notes, “you'll update the URL with the search params, data will be fetched on the server, and only the results that match your query will be returned”. Because the filters are encoded in the URL, the view is shareable/bookmarkable (a key benefit of this pattern). Users can copy the URL and others will see the same filtered results.

We take care to synchronize form state with URL state. For example, on mounting we read current `searchParams` and set form default values (e.g. `<Input defaultValue={searchParams.get('query') || ''} />`) so the filter UI reflects any existing filters. The Zod schema helps here too: we can parse `searchParams` through Zod to get a typed filters object. A “Reset” or “Clear” button will remove all relevant query params (e.g. `params.delete('status')` etc.) and replace the URL with the base route. Closing the filter panel is done via the panel’s own close trigger (e.g. a “X” button or clicking outside).

**Usage flow:** open filter panel → set criteria → submit → update URL params → server fetches new data → table rerenders. Filtering often resets pagination to page 1. Our code ensures that if filters change, the current cursor or page resets, so we always show the first page of the new filtered set.

## Cursor-based Pagination with URL State

For listing pages, we moved beyond simple page numbers to **cursor-based pagination**. Using database cursors (e.g. Prisma’s `cursor` + `take`), we can efficiently paginate large datasets without expensive offsets. The principle is: keep track of a “cursor” value (typically the last or first item’s unique ID on the current page) and use that to fetch the next batch. In our implementation, each page shows 10 records by default. We store pagination state in query params (for sharable links) and also in component state to manage the “Next”/“Previous” controls.

A common pattern we use is:

- **Next page:** take the ID of the last item on the current page, set `cursor={ id: lastId }` and `take=10` with `skip: 1` (to skip the cursor row), e.g. `findMany({ take: 10, skip: 1, cursor: { id: lastId }, orderBy: { id: 'asc' } })`.
- **Previous page:** take the ID of the first item on the current page, set `cursor={ id: firstId }` and `take=-10`, `skip: 1` (negative `take` fetches preceding records), e.g. `findMany({ take: -10, skip: 1, cursor: { id: firstId }, orderBy: { id: 'asc' } })`.
- We add a `dir=next` or `dir=prev` flag in the URL to indicate direction.

On the server side, our code inspects these params and queries accordingly. Cursor pagination is fast because it leverages the database’s index on ID; as one explanation notes, “Cursor-based pagination uses `cursor` and `take` to return a limited set of results before or after a given cursor. A cursor bookmarks your location in a result set and must be a unique, sequential column”. We ensure the results are sorted by ID (or timestamp) so cursors work predictably. When navigating forward, the new cursor becomes the last ID; when navigating backward, the cursor is the first ID of the current page and a negative `take` fetches the previous items.

In the UI, we use React state to track if a page request is in-flight and whether more pages exist. The “Next” and “Previous” buttons call functions that update the URL with new `cursor` and `dir` params. Because these are in the URL, links are shareable. We disable “Next” or “Prev” when at the ends of the dataset (e.g., if fewer than 10 items are returned or we explicitly count totals).

Below the table we display something like “Showing records 11–20” or “Page 2 of N” if we compute total pages. We fetch the total count (via a separate query) when needed so we can show “Page X of Y”. Some implementations derive total pages by dividing count by page size; we include that if available. One StackOverflow answer suggests returning a `count` from the API to enable this. In any case, our approach blends cursor and offset concepts: we use cursors for queries but also maintain count for UI.

**Comparison to offset pagination:** We prefer cursor-based because it scales better on large tables. Offset (`skip`) can become slow or inconsistent on concurrent updates. As described, “Offset pagination does not scale at a database level”, whereas cursor pagination is typically faster (at the cost of requiring a fixed sort order).

## Modal Dialogs for Dynamic Actions

For actions like _viewing_, _editing_, or _confirming delete_, we use responsive dialog modals. In Shadcn/UI, the [`<Dialog>`](https://ui.shadcn.com/docs/components/dialog) component serves as an accessible modal wrapper. As one writeup notes, a dialog is “a window overlaid on … the content underneath inert… basically [a] modal component”. We leverage this to create dynamic modals anywhere in our app.

For example, clicking an “Edit” button might open a dialog containing the same form used on a full page, but inside a popup. We structure it like:

```jsx
<Dialog>
  <DialogTrigger asChild><Button>Edit</Button></DialogTrigger>
  <DialogContent className="sm:max-w-md"> 
    <DialogHeader>
      <DialogTitle>Edit Record</DialogTitle>
      <DialogDescription>Change values as needed.</DialogDescription>
    </DialogHeader>
    <MyForm initialData={rowData} onSubmit={...} />
  </DialogContent>
</Dialog>
```

This pattern ensures the modal is responsive (we set max-width classes for small screens) and accessible (focus is trapped inside). We also define custom close buttons via `<DialogClose asChild>`. For delete confirmations, we use a similar dialog with descriptive text and “Confirm”/“Cancel” buttons.

A nice aspect of Shadcn’s Dialog is that it can wrap other components. For instance, if we have a context menu or dropdown with a “Delete” item, we can enclose that in `<DialogTrigger>` to launch the modal. This means from the table, a user can right-click or click a menu and the dialog pops open. By centralizing dialog usage, all our modals share common styling and behavior.

**Key benefits:** dialogs are easy to reuse (we can even build a dialog provider or hook for global modals), they keep the user on the same page (avoiding navigation), and they handle responsive layouts automatically. We only render the modal’s content when triggered, keeping the DOM clean. This approach provides a polished UX: dynamic forms and views pop up without page reloads, giving the feel of a single-page app.

## Debouncing and Optimized API Calls

To reduce server load and improve latency, we carefully **debounce expensive requests**. Whenever we update query params on user input (especially in search boxes), we avoid doing so on every keystroke. As the Next.js tutorial warns, if we update on every keypress we end up “querying your database on every keystroke!”. In a test, typing “Delba” caused five rapid requests:

```
Searching... D  
Searching... De  
Searching... Del  
Searching... Delb  
Searching... Delba  
```

We prevent this by using a debouncing utility. For example, using the `useDebouncedCallback` hook (from the **use-debounce** package) we wrap the search logic:

```js
const debouncedSearch = useDebouncedCallback((term) => {
  // update URL params with term
}, 300);

<input onChange={e => debouncedSearch(e.target.value)} />
```

Now the function runs only 300ms after the user stops typing. This yields a single request: “Searching... Delba”. By throttling input handling, we dramatically lower the number of server calls for high-frequency events. We apply this debouncing to search inputs, filter changes, or any auto-suggestion fields.

Additionally, our use of server actions and pagination further optimizes fetching. Since most data comes from server components, we rely on React’s streaming and partial hydration: only minimal data is loaded on the client. When possible we also cache queries or use incremental static regeneration for public share routes (below).

**Takeaway:** Debouncing input events (as shown above) is a simple but crucial optimization. It ensures smoother UX and lower latency. Combined with efficient querying (cursor pagination) and caching, our app remains responsive even with complex filtering and large datasets.

## Soft Deletes, Application History, and Audit Logs

Rather than permanently deleting records, we implement **soft deletes**. Each table (e.g. users, companies, applications) has a flag or timestamp column (often `deletedAt`) that marks an item as “deleted” without removing it. When a delete action is performed, we do a server update setting this flag. All our queries by default include a filter to exclude soft-deleted records. This ensures “deleted” items don’t appear in normal lists. However, because they remain in the database, administrators can later view or restore them.

For example, an “Applications” page might have a toggle or separate view for “Archived Applications” that explicitly queries `where: { deletedAt: { not: null } }`. Users can then audit or undelete if needed. This design provides safety (undoing mistakes) and preserves historical data. One implication is that our “delete” modals mention that the record is being archived, not permanently erased.

Alongside soft deletes, we maintain **user activity logs**. Whenever a user performs a create, update, or delete (soft) operation, we append an entry to a logs table: typically `{ userId, actionType, entity, entityId, timestamp, details }`. This creates an auditable trail of who did what. We can display these logs in an “Activity” or “History” tab on each record’s page. For example, under a company’s detail view, an admin might see that “Alice updated the company name on Jan 10, 2025” or “Bob deleted this application on Feb 5, 2025”. This not only aids debugging but can be vital for compliance in enterprise apps.

By keeping soft-deleted rows and a complete log, we ensure **traceability**. Analysts or support staff can track data changes over time. It also allows generating analytics later (e.g. how many items were archived per month). In summary, rather than irreversibly losing data, we treat deletes as reversible and always record them.

## Public Shareable Routes (Token-Based Access)

For certain use cases we provide **public, shareable links**. For instance, a company might want to share a summary of their data with clients or partners without requiring those users to log in. We achieve this by generating unique share tokens. When creating a record (e.g. a company profile or application result), we generate a random UUID or hash token associated with it. We then offer a “Copy share link” button that points to a route like `/share/[token]`.

The Next.js route `/share/[token]/page.tsx` is a special server page marked `'use server'` that takes `params.token`. It looks up the corresponding entity (verifying the token exists and is not expired). If valid, it renders a read-only view of that entity’s data. No authentication is needed, only possession of the token. Because it’s just a server-rendered page, we can still use our regular components (tables, cards, etc.) to display data, but hide any editing controls.

This mechanism is secure as long as tokens are unguessable (we use 128-bit random tokens). If needed, tokens can expire after a time or be revoked by regenerating on the server. We also ensure that these public pages don’t expose sensitive admin data (they show only what’s intended for sharing). For example, a share link for an application view might show status and scores, but not internal comments.

Sharing is smooth: the generated URL is based on our domain and works anywhere. Users do not need to sign up or have an account. Under the hood, the implementation is straightforward: use dynamic routing (`/app/share/[token]/page.tsx` in Next.js) and look up by token. This pattern is similar to many “share” features in apps (Google Docs, etc.) where a token unlocks view rights. Overall, it’s a powerful way to give external stakeholders controlled access to specific data slices.

## Reusability and Consistent Patterns

A central philosophy of our system is to **maximize reuse**. Every piece—from the form logic to table layout to filter form—is built to be easily replicated:

- **Forms:** By standardizing on `useActionState` and one Form component (with Zod validation), creating a new form usually involves only writing the Zod schema and server action. The UI state (errors, success messages, loading) is handled generically. We often even reuse the same form component for “Add” and “Edit” by passing initial values.
    
- **Tables:** We created a generic `<DataTable>` component as described above. To make a new table route, developers import this component, define columns (usually by copying an existing file and tweaking fields), and supply a data-fetching function on the server page. The table markup, pagination buttons, and styles are already in place.
    
- **Filters:** Our filter panel is built as a configurable wrapper around Shadcn forms. A new page can define a Zod schema and fields to use for filtering; the shared filter component takes care of rendering labels, inputs, and wiring them to URL params. We also reuse the same state-parsing logic (transforming `searchParams` into a typed object via Zod) across pages.
    
- **Dialogs:** We use the same Dialog component and CSS classes throughout. If a new route needs a confirmation or detail view, we use our standard modal triggers and content layout. In fact, for complex modals we sometimes implement a modal provider (as suggested by some shadcn UI patterns) to allow opening dialogs from anywhere in the app statefully.
    
- **Pagination State Hook:** We wrote a small hook to encapsulate page cursor logic, so individual pages don’t have to reimplement next/prev link generation. This hook reads `searchParams`, computes `currentCursor`, `currentPage`, and returns functions to go next/prev. We use React state to track pending transitions (so we can disable buttons with the `isPending` flag from `useActionState` if we’re calling it in a transition).
    

Because each feature follows the same blueprint, new routes can often be built by copying an example route and adjusting the model name, schema, and columns. This also means the user experience is very consistent. Actions behave the same way on all pages: forms look the same, tables have the same styling, filters open from the same side panel, etc.

**Developer Experience:** Although the setup took time (figuring out `useActionState`, writing the table template, etc.), the payoff is a codebase where duplication is minimal. We invested time reading documentation and experimenting so that future pages are simple to implement. The effort is evident in boilerplate code: most of the logic resides in our shared components. For instance, error-handling and loading states in forms are done by the same `useActionState` wrapper everywhere.

**User Experience:** The consistent structure also aids usability. Users learn once how filters work or what a dialog looks like, and it’s the same across different parts of the app. Performance is optimized (with debouncing, cursor pagination) so even with many records, the UI stays snappy.

## Conclusion

In building this data-driven application, we prioritized **scalability** and **maintainability**. We implemented advanced patterns—server actions with `useActionState` forms, TanStack tables with pagination, zod-validated filters in URL params, and shareable public pages—to create a robust platform. Each feature was designed with future reuse in mind: new resource routes can borrow the form-and-table structure effortlessly. By debouncing inputs and using efficient cursor queries, we ensure responsive UX. By soft-deleting and logging everything, we keep our data integrity and audit trails sound. And by providing share tokens, we balance security with flexibility for external stakeholders.

This integration of patterns means the application can grow rapidly. Developers have a **clear blueprint**: define a data schema, plug in shared components, and enjoy a polished interface out-of-the-box. The result is a system that is both powerful and easy to extend, reflecting a philosophy of thoroughness and DRY (Don’t Repeat Yourself) design.

**Sources:** We followed best practices from React’s documentation on form state, Shadcn UI’s guides on tables and dialogs, Next.js tutorials on search and pagination, and Prisma documentation on pagination. These informed our implementation details and optimizations.

# Deployment and Future

Manit and kartik zindabad
