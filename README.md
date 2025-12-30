# Bharat Unfolded

*Where Temples Tell History*

A production-ready web application for exploring India's cultural heritage and temple architecture through interactive discovery and AI-powered historical insights.

##Website Link : bharat-unfold.vercel.app

## 1️⃣ Project Overview

**Bharat Unfolded** serves as a digital gateway to India's rich architectural and spiritual heritage. It addresses the challenge of making India's vast temple history accessible to global audiences by combining curated archival data with intelligent, context-aware AI assistance.

**Problem Solved:** Traditional heritage information is fragmented and static. Bharat Unfolded unifies this into an interactive experience.
**Target Users:** Heritage enthusiasts, travelers, history students, and cultural researchers.
**Status:** Production-Ready (V1.0)

## 2️⃣ Core Features

### 🏛️ Heritage & Temple Discovery
Comprehensive database of Indian temples with detailed architectural and historical metadata.
- **Smart Filtering**: Filter by Dynasty (Chola, Pallava), Era, State, or Deity.
- **Rich Media**: High-fidelity image galleries and architectural breakdowns.

### 🤖 Intelligent AI Guide
Context-aware historical consultation powered by LLMs.
- **Contextual Awareness**: The AI understands precisely which temple the user is viewing.
- **Secure Sessions**: Chat history is persisted securely via server-side session management.

### 🛡️ Resilient Data Handling
Built for reliability in uncertain network conditions.
- **Fallback Systems**: Automatic degradation to mock data if primary databases are unreachable.
- **Error Boundaries**: Global React error handling prevents white-screen crashes.

### ⚡ Scalable API Design
- **RESTful Architecture**: Clean separation of concerns.
- **Rate Limited**: Token-bucket protection on all public endpoints.
- **Validated**: Strict Zod schema validation for all inputs.

## 3️⃣ System Architecture

The application follows a strict **Client-Server** separation model for security and performance.

### Client Layer (Frontend)
- **Tech**: Next.js 15 (App Router), React, TypeScript, Tailwind CSS.
- **Responsibilities**: UI rendering, interactive maps, static content display.
- **State**: Stateless components; data fetching via Hooks/Suspense.

### Server Layer (Backend)
- **Tech**: Next.js API Routes, Prisma ORM, Supabase (PostgreSQL).
- **Responsibilities**: Authentication, sensitive data processing, AI orchestration, Rate Limiting.
- **Security**: The "Trust Boundary" lies here. No secrets leak to the client.

### API Routes
- `/api/chat`: AI consultation endpoint (protected, rate-limited).
- `/api/chat/session`: Secure session management (GET/POST/DELETE).
- `/api/db-check`: Health check and connectivity monitoring.
- `/auth/callback`: OAuth security handlers.

### External Services
- **Database**: Supabase (PostgreSQL with RLS).
- **AI Inference**: OpenAI (proxied via Server).
- **Maps/Media**: Leaflet / Supabase Storage.

## 4️⃣ Scalability & Performance

### Caching Strategy
- **Edge Caching**: Static assets and pages are cached at the CDN edge (Vercel).
- **Data Efficiency**: Efficient Prisma queries with select-only projections to minimize payload size.

### Stateless Design
- **Zero Local State**: The server is fully stateless. User sessions are managed via database lookups and JWTs, enabling infinite horizontal scaling of server instances.

### Cost-Aware Scaling
- **Controlled AI**: Rate limits restrict expensive AI calls per IP.
- **Optimized Assets**: Next.js Image optimization reduces bandwidth costs.

## 5️⃣ Security & Best Practices

### Server-Side Protection
- **Secret Management**: API keys (OpenAI, Supabase Service Role) stay strictly on the server.
- **Proxy Pattern**: The Client never calls OpenAI directly; it requests the Server, which authenticates and proxies the call.

### Safe Data Handling
- **Input Validation**: All API bodies are validated with `Zod` schemas before processing.
- **Sanitization**: Output encoding prevents XSS.
- **Row Level Security (RLS)**: Database policies enforce potential access control at the engine level.

### Rate Limiting
- **Defense Depth**: Custom in-memory token bucket limiter prevents abuse of the Chat and Auth APIs.

## 6️⃣ Reliability & Fault Tolerance

### Graceful Degradation
If the database or AI service goes down:
1.  **UI**: Shows a friendly "Offline/Error" state, not a crash.
2.  **Data**: Falls back to static/mock content where permitted (e.g., Explore page).

### Timeouts & Isolation
- **Strict Timeouts**: OpenAI calls have a 30s hard timeout to prevent hanging connections.
- **Failure Isolation**: A failure in the Chat system does not break the Explore or Maps features.

## 7️⃣ Deployment Readiness

- **Platform Agnostic**: Runs as a standard Node.js app (Docker supported) or Serverless (Vercel).
- **Production Tested**: `npm run build` passes with strict type checking.
- **Config**: Consolidated environment variables (12-factor app compliant).

## 8️⃣ Future Enhancements

- **Observability**: Integration with Datadog/Sentry for structured log aggregation.
- **Distributed Rate Limiting**: Migrate from in-memory to Redis (Upstash) for multi-region consistency.
- **Feature Expansion**: User-generated content (reviews/photos) and multi-language AI support.

---
*Maintained by the Bharat Unfolded Engineering Team.*
