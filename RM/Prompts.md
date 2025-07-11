# 1

- `tree --gitignore`
- `package.json`
- maybe also index.ts

Resume manager is a platform for students to look at available job posts. Save their resumes. Apply with applications (one resume). Look at events and notifications. Handle authentication (password). View application status.

But majority of it's magic lies in the admin module. Where users with multiple authorities can perform various operations on jobposts, notifications, applications, students, courses, and everything related to that.

There currently exist 5 major RBAC roles. Namely Superadmin, admin, PC, Result, Student. Each has customizable accesses to various CRUD operations on all the routes.

Superadmin also specially takes care of exporting student data, and adding new student batches via excel import. Add their academic details. Debar bulk students, and update application status on students by using data supplied by company. We can also export applications for a jobpost, and also make a sharable link with public access for companies to look at. Making sure data isn't tempered with.

We also add companies data as they come. And can also view, delete, update, create data. Filtering and pagination is implemented throughout the application.

Courses and branches are data tables instead of enums, to handle future changes without any issues. We can also debar passout all with the single command.

All that, with every action logged including file, app, system is the encapsulation of resume manager. Handled by training and placement department.

# 2


Now I want you to create a synopsis for this project. I worked on the frontend. Here is the structure I intend to follow.

[[Structure]]

This synopsis needs to be at least 30-40 pages. So let's write one by one with each major topic. Starting with Why work on RM? It should around 2-3 pages. i.e. around 1000 words. and proper spacing and formating.

Here are the crucks

- PHP
- Scalability Issue
- Data Migration
- Fragile Physical servers
- How to integration latest technologies and implement changes
- Fixed permissions
- Shit deployment and insecure.
- Prone to scams
- Slow and exhaustive process on uploading bulk data.

We plan on building RM with latest technologies, fast paced agile team working on different sectors to build a scalable secure fast application. With enhances UIUX. No change of scam as completely traceable. Automation of backend process such as bulk upload using excel sheet.

Challenges

- Design scalable architecture (optional)
- Stakeholders Alignment
- Data migration (excel conversion)

Team structure

- We made a team of 4 developers. Two on frontend and two on backend. And later expanded frontend team into a team of 3 senior and 9 junior developers. With a backend head, a frontend head, and an integration head. And went from designing to deploying the application to auto-scale.
- We modularized frontend and backend responsibilties to increase security among developers and construct a formal development environment with specific roles assigned, to avoid confusion down the line.
- Two separate github repositories were made. A single head for appointed for supervision of the entire app. And other was chosen to handle deployment and system design related issues. Docker.
- Every teammate understood their role and took responsibility.

It took us around a month to design initial structure of backend. And then we started with the frontend and integration. But later due to requirement changes, backend had to go through major changes. Which broke the integration with the frontend. Hence the work multiplied. And did second iteration of backend and as well as integration. To meet promised deadline, we made the decision to expand our team and include junior developers. Which also ensures future maintainance of project, even after senior developers pass out. We took management roles and divided work and responsibilty. And completed the entire application in just under 3 months.

Now the RM looks secure and will last at least a decade before any major implementation of infrastructor.

# 3

```
{

"name": "frontend",

"version": "0.1.0",

"private": true,

"scripts": {

"dev": "next dev",

"build": "next build",

"start": "next start",

"lint": "next lint",

"format": "prettier --write ."

},

"dependencies": {

"@emotion/react": "^11.14.0",

"@hookform/resolvers": "^5.0.1",

"@radix-ui/react-alert-dialog": "^1.1.14",

"@radix-ui/react-avatar": "^1.1.3",

"@radix-ui/react-checkbox": "^1.2.3",

"@radix-ui/react-collapsible": "^1.1.4",

"@radix-ui/react-dialog": "^1.1.14",

"@radix-ui/react-dropdown-menu": "^2.1.7",

"@radix-ui/react-icons": "^1.3.2",

"@radix-ui/react-label": "^2.1.2",

"@radix-ui/react-popover": "^1.1.11",

"@radix-ui/react-scroll-area": "^1.2.4",

"@radix-ui/react-select": "^2.2.5",

"@radix-ui/react-separator": "^1.1.3",

"@radix-ui/react-slot": "^1.2.3",

"@radix-ui/react-switch": "^1.2.2",

"@radix-ui/react-tabs": "^1.1.3",

"@radix-ui/react-toast": "^1.2.6",

"@radix-ui/react-tooltip": "^1.2.0",

"@tanstack/react-table": "^8.21.2",

"class-variance-authority": "^0.7.1",

"clsx": "^2.1.1",

"cmdk": "^1.1.1",

"date-fns": "^3.0.0",

"lucide-react": "^0.485.0",

"next": "^15.2.4",

"next-themes": "^0.4.6",

"react": "^18.2.0",

"react-day-picker": "^8.10.1",

"react-dom": "^18.2.0",

"react-dropzone": "^14.3.8",

"react-hook-form": "^7.55.0",

"react-icons": "^5.5.0",

"sonner": "^2.0.5",

"tailwind-merge": "^3.0.2",

"tailwindcss-animate": "^1.0.7",

"zod": "^3.25.67"

},

"devDependencies": {

"@eslint/eslintrc": "^3",

"@types/node": "^20",

"@types/react": "^19",

"@types/react-dom": "^19",

"autoprefixer": "^10.4.21",

"eslint": "^9",

"eslint-config-next": "15.1.7",

"eslint-config-prettier": "^10.1.1",

"eslint-plugin-prettier": "^5.2.5",

"postcss": "^8.5.4",

"prettier": "^3.5.3",

"prettier-plugin-tailwindcss": "^0.6.11",

"tailwindcss": "^3.4.17",

"typescript": "^5"

}

}

```

This is my package.json. Now help me write around 5 - 8 pages. i.e. around 3000 words. On what tech stack did I use. And DIdn't I use it's alternative? For example, why use NextJS, not angular or simply reactJS for frontend? Because of NextJS additional features, like like file based routing. And also familiarity with tech stack like reactjs and nextjs.

We used ShadCN for UI components consistently throughout the application for a simple minimalistic look and headless UI. We used shadCN because it's ease of use and amazing compatibility of nextJs. also local free installation.

Feel free to add more points that you can find. Simiarly explain all the tech stack with props and some concs.

Proper use of zod and typescript for consistent schema validation for backend integration. Making sure no errors in production and handle edge cases using development.

Tailwind CSS for quick UI changes.

Sonner for toaster.

ESlint for error detecting.

Prettier for consistent formatting

lucide reactor for icons. etc.

# 4

### Application Logic


This is my file structure of nextjs frontend.

```bash
resume-manager-frontend on  main [$!] via 🐳 desktop-linux via  v24.2.0 
❯ tree --gitignore
.
├── components.json
├── Dockerfile
├── eslint.config.mjs
├── mds
│   ├── acknowledgement.md
│   ├── oldTodo.md
│   ├── pending.md
│   ├── remarks.md
│   └── roles.md
├── next.config.ts
├── package-lock.json
├── package.json
├── postcss.config.mjs
├── postcss.config.ts
├── public
│   ├── dtuBg.jpg
│   ├── dtuCover.jpeg
│   ├── dtulogo.svg
│   ├── file.svg
│   ├── globe.svg
│   ├── log-in.jpg
│   ├── logout-arrow.png
│   ├── next.svg
│   ├── student-tnp.webp
│   ├── user.svg
│   ├── vercel.svg
│   └── window.svg
├── README.md
├── schema.prisma
├── src
│   ├── app
│   │   ├── (auth)
│   │   │   ├── layout.tsx
│   │   │   └── login
│   │   │       ├── actions.ts
│   │   │       └── page.tsx
│   │   ├── (share)
│   │   │   └── shareApplications
│   │   │       ├── action.ts
│   │   │       ├── columns.tsx
│   │   │       ├── data-table.tsx
│   │   │       ├── layout.tsx
│   │   │       └── page.tsx
│   │   ├── (user)
│   │   │   ├── account
│   │   │   │   ├── actions.ts
│   │   │   │   └── page.tsx
│   │   │   ├── applications
│   │   │   │   ├── action.ts
│   │   │   │   ├── actions.ts
│   │   │   │   ├── columns.tsx
│   │   │   │   ├── data-table.tsx
│   │   │   │   └── page.tsx
│   │   │   ├── dashboard
│   │   │   │   ├── actions.ts
│   │   │   │   └── page.tsx
│   │   │   ├── error.tsx
│   │   │   ├── jobs
│   │   │   │   └── page.tsx
│   │   │   ├── layout.tsx
│   │   │   ├── loading.tsx
│   │   │   ├── profile
│   │   │   │   └── page.tsx
│   │   │   └── resume
│   │   │       ├── actions.ts
│   │   │       └── page.tsx
│   │   ├── admin
│   │   │   ├── (management)
│   │   │   │   ├── academics
│   │   │   │   │   ├── actions.ts
│   │   │   │   │   ├── columns.tsx
│   │   │   │   │   ├── data-table.tsx
│   │   │   │   │   └── page.tsx
│   │   │   │   ├── applications
│   │   │   │   │   ├── actions.ts
│   │   │   │   │   ├── columns.tsx
│   │   │   │   │   ├── data-table.tsx
│   │   │   │   │   └── page.tsx
│   │   │   │   ├── companies
│   │   │   │   │   ├── actions.ts
│   │   │   │   │   ├── columns.tsx
│   │   │   │   │   ├── data-table.tsx
│   │   │   │   │   └── page.tsx
│   │   │   │   ├── courses
│   │   │   │   │   ├── actions.ts
│   │   │   │   │   ├── columns.tsx
│   │   │   │   │   ├── data-table.tsx
│   │   │   │   │   └── page.tsx
│   │   │   │   ├── debarred
│   │   │   │   │   ├── action.ts
│   │   │   │   │   ├── column.tsx
│   │   │   │   │   ├── data-table.tsx
│   │   │   │   │   └── page.tsx
│   │   │   │   ├── jobposts
│   │   │   │   │   ├── actions.ts
│   │   │   │   │   ├── client-page.tsx
│   │   │   │   │   ├── columns.tsx
│   │   │   │   │   ├── data-table.tsx
│   │   │   │   │   └── page.tsx
│   │   │   │   ├── rbac
│   │   │   │   │   ├── actions.ts
│   │   │   │   │   ├── columns.tsx
│   │   │   │   │   ├── data-table.tsx
│   │   │   │   │   └── page.tsx
│   │   │   │   ├── students
│   │   │   │   │   ├── actions.ts
│   │   │   │   │   ├── columns.tsx
│   │   │   │   │   ├── data-table.tsx
│   │   │   │   │   └── page.tsx
│   │   │   │   └── users
│   │   │   │       ├── actions.ts
│   │   │   │       ├── columns.tsx
│   │   │   │       ├── data-table.tsx
│   │   │   │       └── page.tsx
│   │   │   ├── (posts)
│   │   │   │   ├── jobpost
│   │   │   │   │   ├── actions.ts
│   │   │   │   │   └── page.tsx
│   │   │   │   └── notification
│   │   │   │       ├── actions.ts
│   │   │   │       └── page.tsx
│   │   │   ├── (student-action)
│   │   │   │   ├── addstudents
│   │   │   │   │   ├── actions.ts
│   │   │   │   │   └── page.tsx
│   │   │   │   ├── bulk-debar
│   │   │   │   │   ├── actions.ts
│   │   │   │   │   ├── BulkDebarCard.tsx
│   │   │   │   │   ├── BulkDebarForm.tsx
│   │   │   │   │   ├── BulkDebarList.tsx
│   │   │   │   │   └── page.tsx
│   │   │   │   ├── exportrecords
│   │   │   │   │   ├── actions.ts
│   │   │   │   │   ├── ExportApplicationsForm.tsx
│   │   │   │   │   ├── ExportStudentsForm.tsx
│   │   │   │   │   └── page.tsx
│   │   │   │   ├── update-applications
│   │   │   │   │   ├── action.ts
│   │   │   │   │   ├── ApplicationsUpdateForm.tsx
│   │   │   │   │   ├── ApplicationsUpdateUploadCard.tsx
│   │   │   │   │   ├── ApplicationsUpdateUploadsList.tsx
│   │   │   │   │   └── page.tsx
│   │   │   │   └── upload-academic-records
│   │   │   │       ├── AcademicRecordsUploadCard.tsx
│   │   │   │       ├── AcademicRecordsUploadForm.tsx
│   │   │   │       ├── actions.ts
│   │   │   │       ├── current
│   │   │   │       │   └── page.tsx
│   │   │   │       ├── general
│   │   │   │       │   └── page.tsx
│   │   │   │       └── UploadsList.tsx
│   │   │   ├── (system)
│   │   │   │   └── logs
│   │   │   │       ├── app
│   │   │   │       │   ├── columns.tsx
│   │   │   │       │   ├── data-table.tsx
│   │   │   │       │   ├── filter-form.tsx
│   │   │   │       │   └── page.tsx
│   │   │   │       ├── file
│   │   │   │       │   ├── action.ts
│   │   │   │       │   ├── columns.tsx
│   │   │   │       │   ├── data-table.tsx
│   │   │   │       │   ├── filter-form.tsx
│   │   │   │       │   └── page.tsx
│   │   │   │       └── system
│   │   │   │           ├── columns.tsx
│   │   │   │           ├── data-table.tsx
│   │   │   │           ├── filter-form.tsx
│   │   │   │           └── page.tsx
│   │   │   ├── error.tsx
│   │   │   ├── layout.tsx
│   │   │   ├── loading.tsx
│   │   │   └── page.tsx
│   │   ├── api
│   │   │   ├── my-resumes
│   │   │   │   └── route.ts
│   │   │   └── withdraw
│   │   │       └── route.ts
│   │   ├── dummy-data.ts
│   │   ├── favicon.ico
│   │   ├── globals.css
│   │   ├── layout.tsx
│   │   ├── not-found.tsx
│   │   └── page.tsx
│   ├── components
│   │   ├── AcademicForm.tsx
│   │   ├── AccountCard.tsx
│   │   ├── admin
│   │   │   ├── AddStudentsCard.tsx
│   │   │   ├── AddStudentsForm.tsx
│   │   │   ├── AddStudentsList.tsx
│   │   │   ├── ApplicationDetailView.tsx
│   │   │   ├── ApplicationFilterForm.tsx
│   │   │   ├── BatchUploadCard.tsx
│   │   │   ├── BranchCreateForm.tsx
│   │   │   ├── BranchViewDialog.tsx
│   │   │   ├── CompanyCreateForm.tsx
│   │   │   ├── CompanyDeleteDialog.tsx
│   │   │   ├── CompanyDetailView.tsx
│   │   │   ├── CompanyEditForm.tsx
│   │   │   ├── CompanyFilterForm.tsx
│   │   │   ├── CourseCreateDialog.tsx
│   │   │   ├── CourseCreateForm.tsx
│   │   │   ├── CreateCompanyModalButton.tsx
│   │   │   ├── CreateDebarredForm.tsx
│   │   │   ├── CreateJobPostForm.tsx
│   │   │   ├── CreateNotificationForm.tsx
│   │   │   ├── CreateUserForm.tsx
│   │   │   ├── DebarredClientPage.tsx
│   │   │   ├── DebarredFilterForm.tsx
│   │   │   ├── DesktopNavbar.tsx
│   │   │   ├── DesktopSidebar.tsx
│   │   │   ├── DisableBatchDialog.tsx
│   │   │   ├── JobDetailView.tsx
│   │   │   ├── JobEditForm.tsx
│   │   │   ├── JobFilterForm.tsx
│   │   │   ├── JobPostsClientPage.tsx
│   │   │   ├── JobShareModal.tsx
│   │   │   ├── JobToggleDialog.tsx
│   │   │   ├── LogsPage.tsx
│   │   │   ├── MobileNav.tsx
│   │   │   ├── NavGroupItem.tsx
│   │   │   ├── NavItems.tsx
│   │   │   ├── RbacClientPage.tsx
│   │   │   ├── RestoreBatchDialog.tsx
│   │   │   ├── ResumeManager.tsx
│   │   │   ├── RoleCreateDialog.tsx
│   │   │   ├── RoleCreateForm.tsx
│   │   │   ├── RoleDeleteDialog.tsx
│   │   │   ├── SharedApplicationDetailsModal.tsx
│   │   │   ├── StudentAcademicDetails.tsx
│   │   │   ├── StudentBasicDetails.tsx
│   │   │   ├── StudentDetailView.tsx
│   │   │   ├── StudentEditForm.tsx
│   │   │   ├── StudentFilterForm.tsx
│   │   │   ├── StudentToggleStatusDialog.tsx
│   │   │   ├── StudentViewForm.tsx
│   │   │   ├── SystemLogsClientPage.tsx
│   │   │   ├── UserDetailView.tsx
│   │   │   ├── UserEditForm.tsx
│   │   │   ├── UserFilterForm.tsx
│   │   │   └── UserToggleDialog.tsx
│   │   ├── ApplyModal.tsx
│   │   ├── ChangePasswordForm.tsx
│   │   ├── DashboardPage.tsx
│   │   ├── DesktopNavbar.tsx
│   │   ├── DesktopSidebar.tsx
│   │   ├── DetailsModal.tsx
│   │   ├── EventCard.tsx
│   │   ├── EventList.tsx
│   │   ├── InformationPage.tsx
│   │   ├── JobCard.tsx
│   │   ├── JobList.tsx
│   │   ├── MobileNav.tsx
│   │   ├── NavItems.tsx
│   │   ├── NotificationCard.tsx
│   │   ├── NotificationList.tsx
│   │   ├── NotificationTable.tsx
│   │   ├── PersonalForm.tsx
│   │   ├── ResumeUpload.tsx
│   │   ├── RouteProgress.tsx
│   │   ├── SeeMoreModal.tsx
│   │   ├── SharedApplications
│   │   │   ├── ClientWrapperComponent.tsx
│   │   │   └── SharedApplicationsNavbar.tsx
│   │   ├── ui
│   │   │   ├── alert-dialog.tsx
│   │   │   ├── alert.tsx
│   │   │   ├── avatar.tsx
│   │   │   ├── badge.tsx
│   │   │   ├── button.tsx
│   │   │   ├── calendar.tsx
│   │   │   ├── card.tsx
│   │   │   ├── checkbox.tsx
│   │   │   ├── collapsible.tsx
│   │   │   ├── command.tsx
│   │   │   ├── companyViewModal.tsx
│   │   │   ├── custom-modal.tsx
│   │   │   ├── dialog.tsx
│   │   │   ├── dropdown-menu.tsx
│   │   │   ├── form.tsx
│   │   │   ├── input.tsx
│   │   │   ├── label.tsx
│   │   │   ├── popover.tsx
│   │   │   ├── radio-group.tsx
│   │   │   ├── scroll-area.tsx
│   │   │   ├── select.tsx
│   │   │   ├── separator.tsx
│   │   │   ├── sheet.tsx
│   │   │   ├── skeleton.tsx
│   │   │   ├── sonner.tsx
│   │   │   ├── switch.tsx
│   │   │   ├── table.tsx
│   │   │   ├── tabs.tsx
│   │   │   ├── textarea.tsx
│   │   │   ├── tooltip.tsx
│   │   │   ├── under-contruction.tsx
│   │   │   └── use-toast.ts
│   │   └── WithdrawActions.tsx
│   ├── constants
│   │   ├── index.ts
│   │   └── nav.ts
│   ├── lib
│   │   ├── api.ts
│   │   ├── exceptions.ts
│   │   └── utils.ts
│   └── middleware.ts
├── tailwind.config.ts
└── tsconfig.json
```

- API classes - defined custom error handling classes and fetchAPI functions for a more customizable experience instead of using `axois`.
- Error handling - custom class. And global error handling check, to catch any thrown errors in the code, which shows an alern screen, with useful message inside both component and toaster.
- Loading - nextjs provides automatic suspense loading using `loading.tsx`
- Not found - same
- Toasters - toasters are defined in root.tsx for global calling
- Autherization. via refresh token. Use cookies to store access token with validility 15 minutes of security. and refresh token with validity 1 hour. middleware access token isn't expired.
- Authentication (student vs admin) - middle ware ensures to admin is able to access student module. and student can't access or call any admin module apis.
- Index.ts (constants interface, enum) every constand and enum goes here
- Nav.ts (sidebar items route for both web and mobile access)
- Component folders has all components.
- every table is build using data-table, columns, actions.ts, page.ts structure. ensuring consistency.
- Every API call is done in server components. page.tsx or actions.ts. And client components have dynamic UI components. ensuring no hydration error.
- etc, etc.

# 5

Now finally comes integration. This is the bulk of the project. This portion should be around 10-15 pages. i.e. 6000-7000 words. Don't make it concise.

Mainly we cover
- Forms - Using useActionState
- Table - using shadCN table with pagination
- Filter - using forms and query params
- Pagination - using cursor and take from backend and storing in query params. also using useStates to handle next and prev. Total count for current page.
- Custom Modal - for responsive, dynamic dialogs, useful for view, update or delete forms.
- Debounce and optimized api calling, for reduced latency
- Soft-delete, application view, and user logs for traceable history and future analysis.
- Public sharable routes for company application view, using share token

We spend a lot of time optimizing every single major reusable components. So make other routes can follow that route and easily implement similar routes using well defined boilerplate code.

Same was the case with forms. We wanted to handle error, loading, and states on client side. And handle api calling and data fetching on server side actions.ts. After spending a lot of reading documentation. We came upon useActionState which handles most of these things. But doesn't call apis in server component. To overcame this is we used startTransition(form) to call form submit from client side inside a function. Which can be triggered from the client and call onSubmit on backend. And perfectly handles state changes.

Similarly tables follow a consistent structure. Using shadCN template and custom data-tables and columns specific for all routes. We added buttons, dropdowns, dialogs inside these tables for greater UX.

Filter use shadCn filter sheet. to display shadCn forms. using zod validation to handle query params fetching and changing. Using select with nativeEnums. Close trigger, Also reset. And work well with pagination.

Pagination was on the last things that was implemented. Taking a default take of 10 records for single page view. removing user of scrolling. Also storing pages and cursor in query params to make these links sharable. The first record id as cursor and dir = 'prev' gives prev 10 records. where as 10th record id as cursor and div = 'next' gives next 10 records. Using useStates to store prev / next changes. With loading with actions.ts data fetching.

Debounce to implement optimized search throughout all companies return data inside comand shadcn component. for great UX.

Similarly use your brain to write everything that's relavent. 