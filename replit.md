# Teen Tabahi - Idea Tracker

## Overview

Teen Tabahi is a fun idea tracking application designed for a group of three friends (Raunak, Sankalp, and Shivam) to log their startup ideas and track which stage each idea is at. The app has a playful, irreverent tone with Hindi-English mixed language ("Hinglish") used throughout the UI. Ideas can progress through various stages from initial conception to advanced development, or be marked as "Dropped" with a reason and roast message.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Routing**: Wouter (lightweight React router)
- **State Management**: TanStack React Query for server state
- **Styling**: Tailwind CSS with shadcn/ui component library
- **Animations**: Framer Motion for UI animations
- **Form Handling**: React Hook Form with Zod validation
- **Theme**: Light/dark mode support with CSS variables

The frontend follows a component-based architecture with:
- Pages in `client/src/pages/` (login, dashboard, not-found)
- Reusable components in `client/src/components/`
- UI primitives from shadcn/ui in `client/src/components/ui/`
- Custom hooks in `client/src/hooks/`
- Utilities and contexts in `client/src/lib/`

### Backend Architecture
- **Framework**: Express.js 5 with TypeScript
- **Database ORM**: Drizzle ORM with PostgreSQL
- **API Pattern**: RESTful JSON API
- **Build Tool**: esbuild for server bundling, Vite for client

The server follows a layered architecture:
- `server/index.ts` - Express app setup and middleware
- `server/routes.ts` - API route definitions
- `server/storage.ts` - Data access layer using Drizzle
- `server/db.ts` - Database connection pool
- `server/seed.ts` - Sample data seeding

### Authentication
- Simple password-based authentication (hardcoded password: "Ankitlove")
- Session tokens stored in memory on server, sessionStorage on client
- Custom `x-auth-token` header for API authentication
- No external auth providers

### Data Model
Single table `ideas` with fields:
- `id` - UUID primary key
- `name` - Idea name/description
- `owner` - One of three friends (Raunak, Sankalp, Shivam)
- `currentStage` - Stage enum (Idea Stage → Research Stage → Initial Work Stage → Got Started Stage → Advanced Stage → Dropped)
- `dropReason` - Why idea was dropped (if applicable)
- `dropStage` - At which stage it was dropped (if applicable)
- `createdAt` - Timestamp

### Build Process
- Development: `tsx` runs TypeScript directly with Vite dev server
- Production: Vite builds client to `dist/public`, esbuild bundles server to `dist/index.cjs`
- Database migrations: `drizzle-kit push` for schema sync

## External Dependencies

### Database
- **PostgreSQL** - Primary database via `DATABASE_URL` environment variable
- **Drizzle ORM** - Type-safe database queries and schema management
- **pg** - Node.js PostgreSQL driver

### UI Libraries
- **shadcn/ui** - Comprehensive UI component library (accordion, dialog, form, toast, etc.)
- **Radix UI** - Accessible primitives underlying shadcn components
- **Lucide React** - Icon library
- **Framer Motion** - Animation library
- **date-fns** - Date formatting utilities

### Development Tools
- **Vite** - Frontend build tool and dev server
- **esbuild** - Server bundling for production
- **TypeScript** - Type checking across full stack
- **Tailwind CSS** - Utility-first CSS framework