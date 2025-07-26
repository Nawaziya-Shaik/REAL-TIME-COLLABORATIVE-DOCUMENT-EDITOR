# Replit.md

## Overview

This is a Google Docs-style collaborative document editor built with a modern full-stack architecture. The application provides a rich text editing experience using TipTap editor, with real-time collaboration via Socket.IO and MongoDB persistence. It features a clean, minimalist UI inspired by Google Docs with document creation, editing, sharing capabilities, and live collaborative editing.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Styling**: Tailwind CSS with shadcn/ui component library
- **Rich Text Editor**: TipTap with StarterKit extensions
- **State Management**: TanStack Query (React Query) for server state
- **Routing**: Wouter for lightweight client-side routing
- **UI Components**: Radix UI primitives with custom styling

### Backend Architecture
- **Runtime**: Node.js with Express.js
- **Language**: TypeScript with ES modules
- **Database**: MongoDB with native driver (fallback to in-memory storage)
- **Real-time Communication**: Socket.IO for live collaboration
- **Schema Validation**: Zod for type-safe API validation
- **Document Persistence**: MongoDB collections with automatic seeding

### Build System
- **Frontend Bundler**: Vite with React plugin
- **Backend Bundler**: esbuild for production builds
- **Development**: Hot module replacement with Vite dev server
- **TypeScript**: Strict mode enabled with path mapping

## Key Components

### Data Models
- **Documents**: MongoDB documents with id, title, content (TipTap JSON), timestamps
- **Users**: Authentication entity with username/password (prepared but not fully implemented)
- **Content Structure**: TipTap JSON format for rich text content
- **Real-time Events**: Socket.IO events for content changes, title updates, user presence

### Frontend Components
- **DocumentCanvas**: TipTap editor wrapper with content synchronization
- **Header**: Application header with title editing and action buttons
- **Sidebar**: Document navigation with create/delete operations
- **Toolbar**: Rich text formatting controls (prepared for TipTap integration)
- **ShareModal**: Document sharing interface with link generation

### Backend Services
- **Storage Layer**: Abstract storage interface with MongoDB and in-memory implementations
- **API Routes**: RESTful endpoints for document CRUD operations
- **Socket.IO Server**: Real-time collaboration with document rooms and user presence
- **Middleware**: Request logging, error handling, and JSON parsing

## Data Flow

### Document Operations
1. **Creation**: Client POST to `/api/documents` → Validation → Storage → Response
2. **Retrieval**: Client GET from `/api/documents/:id` → Storage lookup → Response
3. **Updates**: Client PATCH to `/api/documents/:id` → Validation → Storage update
4. **Listing**: Client GET from `/api/documents` → Storage query → Response

### State Management
- **Server State**: TanStack Query handles caching, synchronization, and optimistic updates
- **Client State**: React hooks for local UI state (sidebar visibility, modals)
- **Content State**: TipTap editor state synchronized with server via mutations

### Real-time Collaboration
- **Socket.IO Integration**: Live document editing with conflict-free updates
- **User Presence**: Real-time user count and collaboration indicators
- **Document Rooms**: Socket.IO rooms for per-document collaboration
- **Content Synchronization**: Debounced content changes broadcast to all users
- **Title Synchronization**: Real-time title updates across all connected users

## External Dependencies

### Database
- **MongoDB**: NoSQL document database for flexible document storage
- **Environment Variables**: `MONGODB_URL` or `MONGO_URL` for connection
- **Fallback**: Automatic fallback to in-memory storage if MongoDB unavailable
- **Auto-seeding**: Sample documents created automatically on first run

### UI Framework
- **shadcn/ui**: Pre-built accessible components
- **Radix UI**: Headless component primitives
- **Tailwind CSS**: Utility-first styling with custom design tokens

### Development Tools
- **Replit Integration**: Cartographer plugin for development environment
- **Runtime Error Overlay**: Development error handling
- **PostCSS**: CSS processing with Tailwind and Autoprefixer

## Deployment Strategy

### Production Build
- **Frontend**: Vite builds to `dist/public` directory
- **Backend**: esbuild bundles to `dist/index.js`
- **Static Serving**: Express serves built frontend assets

### Environment Configuration
- **Development**: `NODE_ENV=development` with hot reloading
- **Production**: `NODE_ENV=production` with optimized builds
- **Database**: MongoDB connection via `MONGODB_URL` or `MONGO_URL`
- **Real-time**: Socket.IO automatically configured with CORS support

### Scaling Considerations
- Stateless backend design supports horizontal scaling
- MongoDB connection pooling and replica sets for high availability
- Socket.IO Redis adapter can be added for multi-instance real-time support
- Static assets can be served via CDN
- In-memory fallback ensures development works without external dependencies

## Recent Changes (January 26, 2025)

✓ **Real-time Collaboration**: Implemented Socket.IO for live document editing
✓ **MongoDB Integration**: Added MongoDB support with automatic fallback to in-memory storage
✓ **User Presence Indicators**: Real-time user count and collaboration status
✓ **Live Content Sync**: Debounced content changes broadcast to all connected users
✓ **Title Collaboration**: Real-time title editing across multiple users

The architecture prioritizes developer experience with TypeScript throughout, modern tooling, and a clean separation of concerns between frontend, backend, and data layers. The component-based design enables easy feature additions and modifications while maintaining type safety across the entire stack.