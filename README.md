# AI Dispute Resolver

## Overview

This is a full-stack web application that provides AI-powered dispute resolution services. Users can submit agreements and evidence, and the system uses OpenAI's GPT-4o model to analyze the information and provide fair, reasoned decisions with confidence scores and legal recommendations.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **React 18** with TypeScript for the user interface
- **Vite** as the build tool and development server
- **Tailwind CSS** for styling with a custom design system
- **shadcn/ui** component library for consistent UI components
- **Wouter** for client-side routing (lightweight alternative to React Router)
- **TanStack Query** for server state management and API caching

### Backend Architecture
- **Express.js** server with TypeScript
- **RESTful API** design with a single `/api/resolve` endpoint
- **In-memory storage** using a custom `MemStorage` class for development
- **OpenAI API integration** for AI-powered dispute resolution
- **Middleware** for request logging and error handling

### Data Storage Solutions
- **Drizzle ORM** configured for PostgreSQL (schema defined but using in-memory storage currently)
- **PostgreSQL** database schema ready for production deployment
- **In-memory storage** for development and testing purposes
- Database migrations configured in the `./migrations` directory

### Authentication and Authorization
- No authentication system currently implemented
- Session management infrastructure present with `connect-pg-simple`
- Ready for future authentication integration

## Key Components

### Frontend Components
- **DisputeResolver Page**: Main interface for submitting disputes and viewing results
- **UI Components**: Comprehensive set of shadcn/ui components (buttons, forms, cards, etc.)
- **React Query Integration**: Manages API calls and caching
- **Toast Notifications**: User feedback system for success/error states

### Backend Components
- **Routes Handler**: Processes dispute resolution requests
- **Storage Layer**: Abstracted storage interface supporting both in-memory and database implementations
- **OpenAI Integration**: Handles AI model communication for dispute analysis
- **Validation Layer**: Zod schemas for request/response validation

### Data Models
- **Users**: Basic user structure (id, username, password)
- **Disputes**: Core dispute entity with agreement, evidence, decision, confidence, and metadata
- **Validation Schemas**: Type-safe request/response handling

## Data Flow

1. **User Input**: User submits agreement and evidence through the web form
2. **Validation**: Frontend validates input using Zod schemas
3. **API Request**: TanStack Query sends POST request to `/api/resolve`
4. **Server Processing**: 
   - Validates request body
   - Creates dispute record in storage
   - Sends structured prompt to OpenAI GPT-4o
   - Processes AI response and extracts decision data
5. **Response**: Returns structured decision with confidence score and recommendations
6. **UI Update**: Frontend displays results with visual indicators and detailed analysis

## External Dependencies

### AI Services
- **Google Gemini API**: Gemini 2.5 Pro model for dispute resolution analysis  
- **Structured JSON responses** with response schema validation for consistent AI output formatting

### Database
- **Neon Database**: Serverless PostgreSQL provider (configured but not actively used)
- **Drizzle Kit**: Database migrations and schema management

### UI/UX Libraries
- **Radix UI**: Headless component primitives for accessibility
- **Lucide React**: Icon library for consistent iconography
- **Class Variance Authority**: Type-safe CSS class management
- **Embla Carousel**: Carousel functionality (available but not used)

### Development Tools
- **ESBuild**: Fast JavaScript bundler for production builds
- **TSX**: TypeScript execution for development server
- **PostCSS**: CSS processing with Tailwind CSS

## Deployment Strategy

### Build Process
- **Frontend**: Vite builds optimized React bundle to `dist/public`
- **Backend**: ESBuild bundles Node.js server to `dist/index.js`
- **Single Command Deploy**: `npm run build` handles both frontend and backend

### Environment Configuration
- **Development**: Uses tsx for hot reloading and Vite dev server
- **Production**: Serves static files and runs compiled server bundle
- **Database**: Configured for PostgreSQL with environment-based connection strings

### Scaling Considerations
- **Stateless Design**: Server can be horizontally scaled
- **Database Ready**: Easy migration from in-memory to PostgreSQL
- **API Rate Limiting**: Should be implemented for OpenAI API usage
- **Error Handling**: Comprehensive error handling for production reliability

### Environment Variables
- `DATABASE_URL`: PostgreSQL connection string
- `GEMINI_API_KEY`: Google Gemini API authentication key
- `NODE_ENV`: Environment mode (development/production)
