# Chronograph Watch Application

## Overview

A luxury chronograph watch application built with React and Express. The app simulates a high-end timepiece with clock, chronograph (stopwatch), and countdown timer modes. Users can track elapsed time with precision timing, save timer sessions to a database, and view their mission log history. The UI features a dark theme with watch-inspired metallic styling and smooth animations.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Routing**: Wouter (lightweight React router)
- **State Management**: TanStack React Query for server state, React useState for local UI state
- **Styling**: Tailwind CSS with CSS variables for theming, custom watch-specific color palette
- **UI Components**: Shadcn/ui component library (New York style) with Radix UI primitives
- **Animations**: Framer Motion for smooth watch hand movements and transitions
- **Build Tool**: Vite with path aliases (@/ for client/src, @shared/ for shared code)

### Backend Architecture
- **Framework**: Express.js with TypeScript
- **API Design**: RESTful endpoints defined in shared/routes.ts with Zod validation
- **Database ORM**: Drizzle ORM with PostgreSQL dialect
- **Schema Validation**: Zod schemas generated from Drizzle schema using drizzle-zod

### Data Flow Pattern
1. API routes defined in `shared/routes.ts` with input/output schemas
2. Frontend hooks in `client/src/hooks/use-timers.ts` consume these routes via React Query
3. Backend routes in `server/routes.ts` validate requests and call storage layer
4. Storage layer in `server/storage.ts` interacts with database via Drizzle

### Database Schema
Single table `timer_history` tracking:
- `id`: Serial primary key
- `type`: Timer type ('chronograph' or 'countdown')
- `duration`: Duration in milliseconds
- `label`: Optional user-defined label
- `completedAt`: Timestamp (auto-generated)

### Build Configuration
- Development: `tsx` for running TypeScript directly with Vite HMR
- Production: esbuild bundles server, Vite builds client to `dist/public`
- Database migrations: `drizzle-kit push` for schema synchronization

## External Dependencies

### Database
- **PostgreSQL**: Primary database, connected via `DATABASE_URL` environment variable
- **Drizzle ORM**: Type-safe database queries with automatic schema inference
- **connect-pg-simple**: PostgreSQL session store (available but not currently used)

### Frontend Libraries
- **@tanstack/react-query**: Async state management and caching
- **framer-motion**: Animation library for watch hand movements
- **date-fns**: Date formatting for mission log timestamps
- **Radix UI**: Accessible component primitives (dialog, tabs, toast, etc.)
- **lucide-react**: Icon library

### Development Tools
- **Vite**: Frontend build tool with HMR
- **esbuild**: Server bundling for production
- **drizzle-kit**: Database migration tooling
- **TypeScript**: Type safety across the entire stack

### Replit-Specific
- **@replit/vite-plugin-runtime-error-modal**: Error overlay in development
- **@replit/vite-plugin-cartographer**: Dev tooling (development only)
- **@replit/vite-plugin-dev-banner**: Development banner (development only)