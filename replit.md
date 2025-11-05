# Clyra Discord Bot Dashboard

## Overview

Clyra is a web-based management dashboard for a Discord bot designed for Emergency Response: Liberty County (ER:LC) game servers. The application provides server administrators with a comprehensive interface to configure bot modules, manage server settings, and monitor bot functionality. The dashboard features a modern, Discord-inspired design system built with React and TypeScript.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture

**Framework & Build System**
- React 18+ with TypeScript for type-safe component development
- Vite as the build tool and development server
- Wouter for lightweight client-side routing (no React Router dependency)
- React Query (TanStack Query) for server state management and API data fetching

**UI Component Library**
- shadcn/ui component system with Radix UI primitives
- Tailwind CSS for styling with custom design tokens
- Custom color system using CSS variables for theming support
- Component variants using class-variance-authority (CVA)

**Design System**
- Typography: Inter for UI elements, Space Grotesk for display text
- Discord-inspired visual language combined with Linear's dashboard clarity
- Custom spacing primitives using Tailwind's scale (2, 4, 6, 8, 12, 16, 24)
- Hover/active states with CSS variable-based elevation system

**State Management**
- React Query for all server-side data (user info, servers, configurations)
- Session-based authentication with express-session
- Local component state with React hooks

### Backend Architecture

**Runtime & Framework**
- Node.js with Express.js for the HTTP server
- TypeScript throughout with ES modules
- Session-based authentication (no traditional user accounts)

**API Design**
- RESTful endpoints under `/api` prefix
- JSON-based request/response format
- Session cookies for maintaining user state
- Endpoints:
  - `/api/auth/user` - Get current Discord user info
  - `/api/servers` - List user's Discord servers with admin permissions
  - `/api/servers/:id` - Get specific server configuration
  - `/api/servers/:id/modules/:moduleId/toggle` - Toggle module on/off
  - `/api/servers/:id/modules/:moduleId/config` - Update module configuration

**Data Storage**
- File-based JSON storage for server configurations (`server_configs.json`)
- In-memory storage class (`MemStorage`) with file persistence
- Drizzle ORM configured for PostgreSQL (schema defined but not actively used)
- Future migration path to database evident from Drizzle configuration

**Discord Integration**
- OAuth2 authentication via Replit Discord connector
- Direct Discord API calls for user and guild information
- Token refresh handling for expired access tokens
- Permission validation to filter admin-only servers

**Module System**
- Pluggable module architecture with standardized configuration schema
- Each module has: name, description, icon, enabled state, configured state, and custom fields
- Module types: watchai, promotion, bannedcar, runcommand, liverycheck, massrdm, kicktimer
- Premium vs free module differentiation
- Configuration validation using Zod schemas

### Key Architectural Decisions

**Why File-Based Storage Initially**
- Simplifies initial development and deployment
- No database setup required for basic functionality
- Easy to inspect and debug configuration state
- Clear migration path to PostgreSQL via Drizzle when scale requires it

**Why Replit Discord Connector**
- Eliminates need for custom OAuth2 implementation
- Automatic token refresh and credential management
- Seamless integration with Replit hosting environment
- Security benefits from managed credential storage

**Why React Query**
- Automatic request deduplication and caching
- Built-in loading and error states
- Optimistic updates for better UX
- Reduces boilerplate for data fetching

**Why Session-Based Auth Instead of JWT**
- Simpler server-side implementation
- Natural fit with Express.js ecosystem
- Easy session invalidation
- Discord connector provides the user identity

**Why Wouter Instead of React Router**
- Smaller bundle size (1.6KB vs 10KB+)
- Simpler API with hooks-first design
- Sufficient for the app's routing needs
- Better performance for smaller applications

**Component Architecture Pattern**
- Presentational components separate from data-fetching logic
- Reusable UI primitives from shadcn/ui
- Custom business components (FeatureCard, ModuleCard, ServerCard)
- Dialog-based configuration flows for module settings

## External Dependencies

### Third-Party Services

**Discord API (v10)**
- User authentication and authorization
- Guild (server) information retrieval
- Permission checking for admin access
- Avatar and user profile data

**Replit Connectors**
- Discord OAuth2 authentication flow
- Credential storage and token management
- Environment-based configuration

### Database

**Neon Serverless PostgreSQL**
- Configured via `@neondatabase/serverless` driver
- Drizzle ORM for schema management and queries
- Database URL provided via `DATABASE_URL` environment variable
- Connection pooling handled by Neon's serverless driver
- Currently configured but not actively used (file-based storage is primary)

### Key NPM Dependencies

**Core Framework**
- express - Web server framework
- react & react-dom - UI library
- typescript - Type system
- vite - Build tool and dev server

**Discord Integration**
- discord.js - Discord API wrapper (for bot functionality, not dashboard auth)

**UI Components**
- @radix-ui/* - Headless UI primitives (accordion, dialog, dropdown, etc.)
- tailwindcss - Utility-first CSS framework
- lucide-react - Icon library

**Data & Forms**
- @tanstack/react-query - Server state management
- react-hook-form - Form state management
- @hookform/resolvers - Form validation
- zod - Schema validation
- drizzle-orm - Database ORM
- drizzle-zod - Zod schema generation from Drizzle

**Session Management**
- express-session - Session middleware
- connect-pg-simple - PostgreSQL session store (for future use)

**Development Tools**
- @replit/vite-plugin-* - Replit-specific development plugins
- tsx - TypeScript execution for development
- esbuild - Fast bundler for production builds