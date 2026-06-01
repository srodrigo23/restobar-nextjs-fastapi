# Restobar - POS System

A full-stack point-of-sale (POS) web application for a restaurant/bar. The project is split into two main parts: an interactive Next.js frontend and a RESTful API backend built with FastAPI and SQLite.

## Project Architecture

```
restobar-system/
├── client/                 # Frontend (Next.js 15)
│   ├── app/               # Application routes and pages
│   │   ├── (auth)/login/  # Login page
│   │   └── (main)/
│   │       ├── waiter/    # Main waiter ordering interface
│   │       └── admin/     # Admin panel (placeholder)
│   ├── components/        # Reusable UI components
│   ├── context/           # React contexts (OrderContext)
│   ├── util/              # Types and utilities
│   └── middleware.ts      # Route protection (authentication)
├── service/               # Backend (FastAPI)
│   ├── app/
│   │   ├── main.py        # API entry point
│   │   ├── database.py    # SQLModel models and DB config
│   │   └── routes/        # API endpoints
│   └── scripts/           # Development scripts
└── package.json           # Orchestrator for both services
```

## Tech Stack

### Frontend
- **Framework**: Next.js 15 with Turbopack
- **UI Library**: React 19 with TypeScript
- **Components**: HeroUI (@heroui/react), Material UI (@mui/material)
- **Styling**: Tailwind CSS 4, Emotion
- **Forms**: react-hook-form, Zod (validation), @hookform/resolvers
- **Animations**: Framer Motion

### Backend
- **Runtime**: Python 3.12
- **Framework**: FastAPI with Uvicorn
- **ORM**: SQLModel (built on SQLAlchemy)
- **Database**: SQLite

### Dev Tools
- **Concurrently** — runs client and server in parallel
- **pnpm** — package manager

## Features

### Authentication
- Simple login with hardcoded credentials (`admin` / `admin`)
- Cookie-based authentication (`auth-token`)
- Next.js middleware protects `/waiter` and `/admin` routes
- Automatic redirect to login if no active session

### Waiter Interface (`/waiter`)
The core POS functionality, designed for table-side order taking:

- **Category navigation** — tabs to filter the menu:
  - Chicken Wings (Alitas)
  - Craft Beer (Cerveza)
  - Soft Drinks (Refrescos)
  - Cocktails/Drinks (Tragos)

- **Order Management** — React context (`OrderContext`) handling:
  - Adding and removing products
  - Updating quantities
  - Product customization (e.g., sauce selection for wings, fry size)
  - Automatic total calculation in Bolivianos (Bs.)

- **Order Drawer** — full-screen panel showing:
  - Current order summary
  - Quantity controls per item
  - Customization details
  - Running total

### Admin Panel (`/admin`)
- Placeholder page ready for future management features (product management, users, reports, etc.)

### Product API (Backend)
RESTful endpoints with pagination:

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/products` | List products with pagination (offset/limit) |
| `GET` | `/products/{id}` | Get a single product by ID |
| `POST` | `/products` | Create a new product |

### Data Models
- **Product** — menu item with name, price, category, and customization options
- **Order** — represents customer orders (base structure, pending expansion)

## Getting Started

```bash
# Install dependencies
pnpm install

# Start development environment (client + server)
pnpm run dev
```

This runs both services concurrently:
- **Client**: Next.js dev server (Turbopack) at `http://localhost:3000`
- **Server**: FastAPI with auto-reload at `http://localhost:8000`

## Project Status

The waiter module is functional with menu browsing and order management. The admin panel is a placeholder pending further development. The SQLite database is created automatically when the server starts.
