# EduSphere — Advanced School Management System

A full-stack, enterprise-grade **School Management ERP** built with Next.js 16, TypeScript, and Prisma. It digitizes the entire school operational lifecycle — admissions, attendance, fees, examinations, timetable, library, transport, staff, and analytics — in a responsive, multi-tenant SaaS architecture.

![EduSphere Dashboard](https://img.shields.io/badge/Next.js-16-black) ![TypeScript](https://img.shields.io/badge/TypeScript-5-blue) ![Prisma](https://img.shields.io/badge/Prisma-6-indigo) ![Tailwind](https://img.shields.io/badge/Tailwind-4-teal) ![License](https://img.shields.io/badge/License-MIT-green)

---

## Features

### 14 Functional Modules

| # | Module | Highlights |
|---|---|---|
| 1 | **Dashboard** | 4 KPI cards, 4 interactive charts (attendance trend, fee collection, enrollment, revenue vs expense), upcoming events, notifications, quick actions |
| 2 | **Students** | CRUD with dialog forms, profile sheet with tabs, search/filter/pagination, class & section assignment |
| 3 | **Attendance** | Batch marking (present/absent/late), class-wise statistics, individual history |
| 4 | **Fees** | Fee structures, 560+ records, payment collection with auto late-fine & discount, multi-method (UPI/Cash/Bank/Online) |
| 5 | **Examinations** | Exam CRUD, marks entry with auto-grading (A1–E), results with ranking & grade distribution chart |
| 6 | **Timetable** | Weekly grid view (8 periods × 5 days), subject color-coding, teacher workload analysis |
| 7 | **Homework** | Assignment CRUD, due-date tracking, status workflow |
| 8 | **Communication** | Notification center, role-based targeting, message categorization |
| 9 | **Library** | Book inventory, ISBN, issue/return tracking, availability management |
| 10 | **Staff & HR** | Teaching + non-teaching staff, department analytics, salary tracking |
| 11 | **Transport** | Vehicle management, routes, driver info, capacity tracking |
| 12 | **Events** | Event calendar, venue management, type categorization |
| 13 | **Reports** | 4 report types (Attendance, Fees, Academic, Financial) with 10+ charts |
| 14 | **Settings** | School profile (read-only), academic session config, preferences |

### Architecture Highlights

- **Multi-tenant SaaS design** — every entity is school-scoped via `schoolId` foreign key
- **Client-side module routing** via Zustand store with lazy-loaded components (`next/dynamic`, `ssr: false`)
- **26-table relational database** with cascading relations, audit logging, and idempotent seeding
- **20 RESTful API endpoints** (Next.js Route Handlers) with consistent `{ data }` / `{ error }` contract
- **Responsive, mobile-first UI** with shadcn/ui, sticky header & footer, accessibility (ARIA, semantic HTML)
- **Type-safe end-to-end** — TypeScript strict mode, Prisma generated types, Zod runtime validation

---

## Tech Stack

### Frontend
- **Next.js 16** (App Router, Turbopack)
- **TypeScript 5**
- **React 19**
- **Tailwind CSS 4** + **shadcn/ui** (40+ components, New York style)
- **Recharts** (Area, Bar, Pie, Line charts)
- **Zustand** (client state) + **TanStack Query** (server state)
- **React Hook Form** + **Zod** validation
- **Framer Motion** animations
- **Lucide React** icons

### Backend & Database
- **Next.js Route Handlers** (App Router API)
- **Prisma 6** ORM
- **SQLite** database (portable, file-based)
- **NextAuth.js v4** (auth-ready)
- **Bun** runtime

### Tooling
- **ESLint 9** + eslint-config-next
- **Prettier**-compatible

---

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) 18+ or [Bun](https://bun.sh/) 1.1+
- A package manager: `npm`, `pnpm`, `yarn`, or `bun` (recommended)

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/<your-username>/edusphere.git
cd edusphere

# 2. Install dependencies
bun install        # or: npm install

# 3. Configure environment variables
cp .env.example .env

# 4. Initialize the database (creates tables)
bun run db:push    # or: npx prisma db push

# 5. Seed the database with realistic demo data (3,400+ records)
bun run db:seed    # or: bun prisma/seed.ts

# 6. Start the development server
bun run dev        # or: npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

### Demo Data

The seed script (`prisma/seed.ts`) populates the database with a realistic Indian school dataset:
- **1 School** — Delhi Public School, Roorkee
- **80 Students** across 12 classes (Class 1–12, sections A & B)
- **15 Teachers** + **8 Staff** members
- **2,470 Attendance** records (last 30 days)
- **922 Fee records** with realistic paid/pending/overdue distribution
- **40 Timetable** entries, **10 Homework** assignments
- **5 Events**, **10 Notifications**, **22 Library books**, **5 Vehicles**
- Income/expense records, lesson plans, enquiries

---

## Project Structure

```
edusphere/
├── prisma/
│   ├── schema.prisma        # 26 Prisma models (DB schema)
│   └── seed.ts               # Idempotent seed script (3,400+ records)
├── src/
│   ├── app/
│   │   ├── api/              # 20 RESTful API route handlers
│   │   │   ├── dashboard/
│   │   │   ├── students/
│   │   │   ├── attendance/
│   │   │   ├── fees/
│   │   │   ├── exams/
│   │   │   ├── timetable/
│   │   │   └── ... (14 more)
│   │   ├── layout.tsx        # Root layout
│   │   ├── page.tsx          # Home page (dynamic module loader)
│   │   └── globals.css       # Global styles
│   ├── components/
│   │   ├── layout/           # AppShell, Header, Sidebar
│   │   ├── modules/          # 14 feature module components
│   │   └── ui/               # 40+ shadcn/ui components
│   ├── hooks/                # use-toast, use-mobile
│   ├── lib/                  # db client, utils
│   └── store/                # Zustand app store
├── public/                   # logo.svg, robots.txt
├── .env.example              # Environment variable template
├── package.json
├── tsconfig.json
├── tailwind.config.ts
├── next.config.ts
└── README.md
```

---

## Database Schema

26 Prisma models organized by domain:

| Domain | Models |
|---|---|
| **Multi-tenant core** | `School`, `User` |
| **People** | `Student`, `Teacher`, `Staff` |
| **Academics** | `Class`, `Section`, `Subject`, `Timetable`, `Homework`, `LessonPlan`, `Exam`, `Mark` |
| **Attendance** | `Attendance`, `TeacherAttendance` |
| **Finance** | `FeeStructure`, `FeeRecord`, `Payment`, `Expense`, `Income` |
| **Operations** | `Vehicle`, `LibraryBook`, `Event`, `Notification` |
| **Compliance** | `AuditLog`, `Enquiry` |

---

## Available Scripts

| Script | Description |
|---|---|
| `bun run dev` | Start development server on port 3000 |
| `bun run build` | Create production build |
| `bun run start` | Start production server |
| `bun run lint` | Run ESLint |
| `bun run db:push` | Push Prisma schema to database |
| `bun run db:generate` | Generate Prisma client |
| `bun run db:seed` | Seed database with demo data |
| `bun run db:migrate` | Run Prisma migrations |
| `bun run db:reset` | Reset database (destructive) |

---

## API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/dashboard` | KPIs, charts, events, notifications |
| GET/POST | `/api/students` | List (paginated) / Create student |
| GET/PUT/DELETE | `/api/students/[id]` | Student CRUD |
| GET/POST | `/api/attendance` | Attendance records / batch mark |
| GET | `/api/fees` | Fee records with filters |
| POST | `/api/fees/collect` | Process fee payment |
| GET/POST | `/api/fee-structures` | Fee structure CRUD |
| GET/POST | `/api/exams` | Exam list / create |
| GET/PUT/DELETE | `/api/exams/[id]` | Exam CRUD |
| GET | `/api/timetable?sectionId=` | Weekly timetable for a section |
| GET/POST | `/api/homework` | Homework assignments |
| GET/POST | `/api/library` | Library books |
| GET/POST | `/api/transport` | Transport vehicles |
| GET/POST | `/api/staff` | Non-teaching staff |
| GET | `/api/teachers` | Teaching staff |
| GET/POST | `/api/events` | School events |
| GET | `/api/notifications` | Notifications |
| GET | `/api/classes` | Classes & sections |
| GET | `/api/reports` | Analytics data (4 report types) |

---

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

## Author

**Your Name**
- GitHub: [@your-username](https://github.com/your-username)
- LinkedIn: [your-profile](https://linkedin.com/in/your-profile)

---

## Acknowledgments

- [Next.js](https://nextjs.org/) — React framework
- [shadcn/ui](https://ui.shadcn.com/) — UI component library
- [Prisma](https://www.prisma.io/) — Type-safe ORM
- [Tailwind CSS](https://tailwindcss.com/) — Utility-first CSS
- [Recharts](https://recharts.org/) — Charting library
