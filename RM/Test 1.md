**Synopsis: RM – DTU Placement & Resume Manager**

---

## 1. Why RM? (1–2 Pages)

### 1.1 Motivation & Context

Delhi Technological University’s training & placement workflows were fragmented across Excel, email threads, and legacy scripts. This led to inconsistent student records, delayed communications, and heavy manual overhead for the T&P office and recruiters. To address these pain points, we conceived **RM**: a centralized, secure, and role-driven **Resume Manager** and placement portal built on modern web technologies.

### 1.2 Limitations of the Previous System

- **Scattered Data:** Student profiles, applications, and company details lived in multiple disconnected files.
    
- **Manual Scheduling:** Interview slots and application updates were coordinated by email, causing conflicts and missed deadlines.
    
- **No Audit Trail:** Changes to student or application records had no logging, making rollbacks and compliance challenging.
    
- **Rigid Roles:** One-size‑fits‑all permissions forced all admins to share privileges, increasing risk.
    

### 1.3 Our Improvement Plan

1. **Consolidate** all entities—students, resumes, job posts, courses—into a single Prisma-backed database.
    
2. **Automate** common workflows with Next.js API routes and server actions (apply with one click, schedule interviews, generate public shareable links).
    
3. **Enhance UX** using ShadCN/Tailwind CSS, live toasters (Sonner), and inline validation (Zod).
    
4. **Secure & Traceable**: JWT + refresh‑token auth, role‑based access controls (RBAC), and full audit logs for file/app/system actions.
    

### 1.4 Early Challenges

- **Data Migration:** Cleaning inconsistent Excel imports (student batches, academic records).
    
- **Stakeholder Alignment:** Defining which fields matter most to students versus recruiters versus admins.
    
- **Real‑Time Feedback:** Enabling toast notifications and loading states without blocking user flows.
    
- **Permission Granularity:** Architecting five distinct roles with customizable CRUD on hundreds of routes.
    

### 1.5 Team Structure

- **Project Lead:** Architected schema.prisma and Next.js routing conventions.
    
- **Frontend Duo:** Implemented app/(auth), (user), and (admin) modules in React + TypeScript + Next.js.
    
- **Backend Duo:** Built `src/app/api` routes, service classes (`lib/api.ts`), and middleware for errors & auth.
    
- **QA & DevOps:** Automated end‑to‑end tests, Dockerized app, CI/CD on GitHub Actions, Vercel & AWS deployments.
    

---

## 2. Tech Stack Deep Dive (5–8 Pages)

- **Next.js 15 & TypeScript:** File‑based routing under `src/app`, server actions (`actions.ts`), SSR/ISR for SEO.
    
- **Tailwind CSS & ShadCN:** Utility‑first styles plus accessible component library (buttons, dialogs, tables).
    
- **Zod & react-hook-form:** Schema‑driven validation and form state via `useActionState`.
    
- **Sonner Toasters:** Instant feedback on saves, deletes, errors.
    
- **date-fns:** Formatting interview dates and deadlines in localized formats.
    
- **lucide-react & @radix-ui:** Lightweight SVG icons and headless UI primitives (menus, dialogs).
    
- **ESLint & Prettier:** Enforced styles with `eslint.config.mjs` and `prettier-plugin-tailwindcss`.
    
- **Prisma & PostgreSQL:** Typed ORM via `schema.prisma`, migrations for evolving courses & branches.
    
- **Docker & GitHub Actions:** Containerized deployment, lint/build/test pipelines, PR-based merge gating.
    

---

## 3. Application Logic & File Structure (10 Pages)

### 3.1 High‑Level Structure

```
src/app/
 ├─ (auth)/login (layout.tsx, actions.ts)
 ├─ (user)/dashboard, applications, resume, profile
 ├─ (admin)/(management) → academics, companies, jobposts, students, rbac 📑
 ├─ api/ (my-resumes, withdraw)
 ├─ layouts, loading.tsx, error.tsx, not-found.tsx
```

### 3.2 API & Service Classes

- **`lib/api.ts`**: Central fetch wrapper, injects auth token.
    
- **Service Classes** encapsulate CRUD: `StudentService`, `JobPostService`, `NotificationService`.
    
- **Errors** thrown as `APIError` in `exceptions.ts`; global middleware catches & renders JSON.
    

### 3.3 Authentication & RBAC

- **JWT + Refresh Tokens** via HTTP‑only cookies on login.
    
- **Five Roles:** `Superadmin`, `Admin`, `PC`, `Result`, `Student`.
    
- **Role Definitions:** In `constants/index.ts` as enums; permissions stored in DB and loaded into middleware `middleware.ts`.
    
- **Middleware** checks route‑based access: e.g., only Superadmin can import batches or export datasets.
    

### 3.4 Loading, Errors, & Not‑Found

- **`loading.tsx`**: Central Suspense spinner for all async pages.
    
- **`error.tsx` & `not-found.tsx`**: Custom layouts for 404s or unexpected failures.
    

### 3.5 User Feedback & Toasters

Sonner to display:

- Success: "Resume uploaded", "Application submitted"
    
- Warning/Error: "Failed to fetch jobs", "Permission denied"
    

### 3.6 Constants, Enums & Navigation

- **`constants/nav.ts`**: Role‑specific menu items for desktop & mobile nav.
    
- **`constants/index.ts`**: API paths, status enums (`ApplicationStatus`, `UserRole`).
    

---

## 4. Integration Patterns (10–15 Pages)

### 4.1 Data Tables & Pagination

- **`@tanstack/react-table`** displays companies, students, jobposts with sorting & client‑side filters.
    
- **Server‑Side Pagination:** API supports `?page=&limit=`; shown in table footer.
    

### 4.2 Forms & Dialogs

- **Bulk Operations:** Bulk-Debar, BatchStudentImport, ExportRecords in admin’s `(student-action)` folder.
    
- **Custom Modal** (`ui/custom-modal.tsx`): Controlled via context, supports dynamic children and server actions.
    

### 4.3 Debounce & Query Params

- **Search Inputs** use a 300 ms debounce in `utils.ts` to minimize rapid API calls; reflects state in URL for shareable filters.
    

### 4.4 Soft‑Delete & Audit Logs

- **Soft Delete:** Entities marked with `deletedAt`. Toggle restore via dialogs, with confirm prompts.
    
- **Logs:** Three log tables (app, file, system) under `(system)/logs/*`; view filters via date/company/user.
    

### 4.5 Sharing & Public Links

- **Shareable Application Link:** Generates a public token, view-only page under `(share)/shareApplications`, with columns.tsx and data-table.tsx.
    

### 4.6 Caching & Revalidation

- **ISR & SWR:** Company listing pages are revalidated every minute; SWR handles client‑side caching for rapid back‑navigation.
    

---

## 5. Deployment & Git Integration

- **Dockerfile:** Defines Node 24 image, installs dependencies, builds Next.js, and serves via `next start`.
    
- **CI/CD:** GitHub Actions run `lint`, `build`, `test` on PRs; merges trigger deployment to Vercel/production.
    
- **Environment:** Separate `.env.local` for dev, staging, prod; secrets managed via GitHub Secrets/AWS Secrets Manager.
    

---

## 6. Future Roadmap & Maintenance (2 Pages)

### 6.1 Next Features

1. **Analytics Dashboard:** Placement rates, top recruiters, student performance graphs with Recharts.
    
2. **Mobile‑First UI:** Optimize layouts for low‑bandwidth and non‑desktop devices.
    

### 6.2 Maintenance & Team Growth

- **Juniors Onboarding:** Pair programming, code reviews, comprehensive README & mds/roles.md.
    
- **Hierarchical Teams:** Separate frontend, backend, DevOps under clear reporting lines to avoid cross‑conflicts.
    
- **Security Audits & Updates:** Quarterly dependency upgrades, automated Snyk scans, and pen tests.
    

---

_End of Detailed Synopsis for RM._