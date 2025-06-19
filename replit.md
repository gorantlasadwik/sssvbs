# Replit.md

## Overview

This is a full-stack e-commerce application for S V Traders, a spices and dry fruits business. The application is built with a React frontend, Express.js backend, and PostgreSQL database. It provides a customer-facing storefront for browsing products and placing orders, along with an admin dashboard for managing inventory and orders.

## System Architecture

The application follows a monorepo structure with clear separation between client and server code:

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Routing**: Wouter for client-side routing
- **State Management**: TanStack React Query for server state management
- **UI Components**: Radix UI components with shadcn/ui styling
- **Styling**: Tailwind CSS with CSS variables for theming
- **Build Tool**: Vite for development and production builds

### Backend Architecture
- **Framework**: Express.js with TypeScript
- **Database ORM**: Drizzle ORM for type-safe database operations
- **Database**: PostgreSQL (configured for Neon Database)
- **Session Management**: Session-based authentication using connect-pg-simple
- **API Design**: RESTful API with JSON responses

### Project Structure
```
├── client/          # React frontend
│   ├── src/
│   │   ├── components/  # Reusable UI components
│   │   ├── pages/       # Page components
│   │   ├── lib/         # Utility functions
│   │   └── hooks/       # Custom React hooks
├── server/          # Express.js backend
│   ├── routes.ts    # API route definitions
│   ├── storage.ts   # Database abstraction layer
│   └── vite.ts      # Development server setup
├── shared/          # Shared TypeScript types and schemas
│   └── schema.ts    # Database schema and types
└── migrations/      # Database migration files
```

## Key Components

### Database Schema
The application uses four main database tables:
- **Users**: Admin authentication
- **Products**: Product catalog with flexible pricing options
- **Orders**: Customer orders with auto-generated order IDs
- **Order Items**: Individual line items within orders

Products support multiple pricing tiers (per piece, per gram, per 100g, 250g, 500g, per kg) to accommodate different packaging options for spices and dry fruits.

### Authentication System
- Simple session-based admin authentication
- Admin credentials stored in environment variables
- Session state managed in browser sessionStorage

### Product Management
- Category-based product organization (Spices, Dry Fruits)
- Flexible pricing structure supporting various units
- Image upload support with URL storage
- Stock quantity tracking

### Order Processing
- Shopping cart functionality with local state management
- Customer information collection (name, phone, address)
- Order ID generation in format: SVT + YYYYMMDD + sequence
- Order status tracking (Processing, Shipped, Delivered)
- PDF invoice generation using jsPDF
- Order tracking by phone number

### Payment Integration
- Prices stored in paise (smallest currency unit) to avoid decimal precision issues
- Currency formatting utilities for display

## Data Flow

1. **Product Display**: Frontend fetches products from `/api/products` endpoint, optionally filtered by category
2. **Cart Management**: Shopping cart state managed locally in React component state
3. **Order Placement**: Cart items and customer info sent to `/api/orders` endpoint
4. **Order Confirmation**: Server generates unique order ID and stores order details
5. **Admin Management**: Admin can view all orders, update statuses, and manage inventory
6. **Customer Tracking**: Customers can track orders using their phone number

## External Dependencies

### Frontend Dependencies
- **UI Components**: Extensive use of Radix UI primitives for accessibility
- **Icons**: Lucide React for consistent iconography
- **Forms**: React Hook Form with Zod validation
- **PDF Generation**: jsPDF for invoice creation
- **Date Handling**: date-fns for date manipulation

### Backend Dependencies
- **Database**: @neondatabase/serverless for PostgreSQL connection
- **ORM**: Drizzle ORM with Zod integration for type safety
- **Session Storage**: connect-pg-simple for PostgreSQL session storage

### Development Dependencies
- **Build Tools**: Vite for frontend bundling, esbuild for backend bundling
- **TypeScript**: Full TypeScript support across the stack
- **Linting**: ESLint configuration (implied by project structure)

## Deployment Strategy

The application is configured for deployment on Replit with the following setup:

### Development Mode
- Runs on port 5000 with hot module replacement
- Uses Vite dev server for frontend with Express backend
- Database migrations applied via `npm run db:push`

### Production Mode
- Frontend built to `dist/public` directory
- Backend bundled to `dist/index.js` using esbuild
- Static files served by Express in production
- PostgreSQL database required (DATABASE_URL environment variable)

### Environment Variables
- `DATABASE_URL`: PostgreSQL connection string
- `NODE_ENV`: Environment setting (development/production)
- Admin credentials: Configured in application code

### Replit Configuration
- Uses Node.js 20 runtime with PostgreSQL 16 module
- Configured for autoscale deployment
- Port mapping: 5000 (internal) → 80 (external)

## Changelog

```
Changelog:
- June 16, 2025. Initial setup
```

## User Preferences

```
Preferred communication style: Simple, everyday language.
```