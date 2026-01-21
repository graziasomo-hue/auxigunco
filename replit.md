# AUXIGUN Trading Co. Ltd - B2B Export Website

## Overview

This is a professional B2B corporate website for AUXIGUN Trading Co. Ltd, a Sudanese agricultural export company specializing in pulses, cotton, and fodder. The site is designed to project credibility and reliability to international importers, wholesalers, and procurement teams. The primary goal is to generate quote requests and procurement inquiries through a trust-first design approach.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework**: React with TypeScript, using Vite as the build tool
- **Routing**: Wouter for client-side routing (lightweight alternative to React Router)
- **Styling**: Tailwind CSS with custom CSS variables for brand colors (Charcoal #2F343A, Gold #C08A2B)
- **UI Components**: shadcn/ui component library (New York style) with Radix UI primitives
- **Typography**: Playfair Display (serif headings) + Inter (body text)
- **Icons**: Lucide React
- **State Management**: TanStack React Query for server state

### Backend Architecture
- **Runtime**: Node.js with Express.js
- **Language**: TypeScript with ES modules
- **API Structure**: RESTful endpoints under `/api/` prefix
- **Build System**: Custom build script using esbuild for server bundling, Vite for client

### Data Storage
- **Database**: PostgreSQL via Drizzle ORM
- **Schema Location**: `shared/schema.ts` contains all table definitions
- **Tables**: 
  - `users` - User authentication (id, username, password)
  - `quotes` - Quote requests (name, company, email, phone, country, product, quantity, message, timestamps)
- **Migrations**: Drizzle Kit with migrations output to `./migrations`

### Key Design Patterns
- **Monorepo Structure**: Client (`client/`), server (`server/`), and shared code (`shared/`)
- **Path Aliases**: `@/` for client source, `@shared/` for shared code, `@assets/` for attached assets
- **Form Handling**: React Hook Form with Zod validation schemas (generated from Drizzle schemas via drizzle-zod)
- **API Communication**: Centralized fetch wrapper in `queryClient.ts` with error handling

### Page Structure
- Home (single-page with sections: Hero, Products, About, Contact, FAQ, Testimonials, Blog Feed)
  - H1: "Sudanese Cotton, Pulses & Fodder Exporter" (SEO-optimized)
- Product Pages (dedicated pages with detailed specs, CTAs, and category blog feeds):
  - /products/cotton - H1: "Sudanese Cotton Supplier & Exporter"
  - /products/pulses - H1: "Sudanese Pulses & Sesame Supplier & Exporter"
  - /products/fodder - H1: "Sudanese Animal Fodder Supplier & Exporter"
- About (company information)
- Contact (quote request form)
- Thank You (post-submission confirmation)

## External Dependencies

### Database
- **PostgreSQL**: Primary database, connection via `DATABASE_URL` environment variable
- **Drizzle ORM**: Type-safe database queries and schema management
- **connect-pg-simple**: PostgreSQL session storage (available but sessions not currently implemented)

### Third-Party Libraries
- **@tanstack/react-query**: Server state management and caching
- **react-hook-form**: Form state management
- **zod**: Runtime validation schemas
- **drizzle-zod**: Generate Zod schemas from Drizzle table definitions
- **date-fns**: Date formatting utilities

### Build & Development
- **Vite**: Frontend build tool with HMR
- **esbuild**: Server-side bundling for production
- **tsx**: TypeScript execution for development

### Replit-Specific Plugins
- **@replit/vite-plugin-runtime-error-modal**: Error overlay in development
- **@replit/vite-plugin-cartographer**: Development tooling (dev only)
- **@replit/vite-plugin-dev-banner**: Development banner (dev only)
- **vite-plugin-meta-images**: Custom plugin for OpenGraph image URLs

## SEO Implementation

### Meta Tags & OpenGraph
- Comprehensive meta tags in `client/index.html` including title, description, keywords, author, robots, canonical URL
- OpenGraph tags for Facebook/LinkedIn sharing (og:title, og:description, og:type, og:url, og:site_name)
- Twitter Card meta tags for Twitter sharing
- Canonical URL set to https://www.auxigunco.com/

### Structured Data (JSON-LD)
- **Organization Schema**: Company info, contact points, social media links
- **LocalBusiness Schema**: Business hours, address, contact information
- **Product ItemList Schema**: Product catalog with descriptions and categories
- **FAQ Schema**: Dynamically generated in the FAQ component on home page

### Technical SEO
- **robots.txt**: Located at `client/public/robots.txt` with sitemap reference
- **Image Optimization**: All images have descriptive alt text for accessibility and SEO
- **Lazy Loading**: Product images use native lazy loading
- **Aria Labels**: Social media links have aria-label attributes for accessibility

### Social Media Integration
- Facebook: https://facebook.com/Auxigun
- Instagram: https://www.instagram.com/Auxigun
- LinkedIn: https://www.linkedin.com/company/auxigun-trading
- YouTube: https://www.youtube.com/@Auxigun
- External Blog: https://www.auxigunco.com/blog

## EmailJS Integration
- **EmailJS**: Sends quote form submissions to graziasomo@gmail.com
  - Service ID: service_9srbxzy
  - Template ID: template_e7d5zsg
  - Public Key: wEamFDjkW4br1I2f3

## WhatsApp Floating Button
- Fixed position bottom-right corner on all pages
- Links to: https://w.app/auxiguntrading
- WhatsApp green (#25D366) with hover animation
- Mobile-responsive (smaller on mobile devices)

## ALTCHA Captcha
- Privacy-friendly CAPTCHA alternative (no Google tracking)
- Widget added above submit button on quote form
- Backend endpoint: GET /api/altcha/challenge
- Secret Key: Stored in ALTCHA_SECRET environment secret

## Blog Feed Integration
- RSS feed from WordPress blog (https://auxigunco.com/blog/feed/)
- BlogFeed component displays latest 3 posts above footer
- Category-specific feeds supported:
  - /api/blog-feed?category=cotton
  - /api/blog-feed?category=pulses
  - /api/blog-feed?category=fodder
- Server-side fetching to avoid CORS issues
- Each product page shows category-filtered blog posts