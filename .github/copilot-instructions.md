Objective: This document provides the technical guidelines, architectural decisions, and phased development plan for the BudgetBite mobile application. It is intended to guide an autonomous AI coding agent (e.g., Cursor AI) through the development process.

1. Guiding Principles
Modularity & Reusability: Code must be organized into small, reusable modules/components with clear responsibilities. Avoid monolithic structures.

Scalability: Design backend services and database schemas with future growth in mind. Use efficient querying and caching strategies.

Security: Implement security best practices from the start. Sanitize inputs, use parameterized queries, manage secrets securely, and implement robust authentication/authorization.

User Experience (UX): Prioritize a clean, intuitive, and responsive user interface. Ensure offline capabilities function seamlessly.

AI-Readiness: Design APIs and data structures to be easily consumable by AI models. Ensure clear documentation and consistent data formats.

Testability: Write code that is easily testable. Strive for high unit and integration test coverage.

Maintainability: Adhere strictly to coding standards, use clear naming conventions, and provide comprehensive documentation (code comments, API docs).

2. Technology Stack & Architecture
Frontend:

Framework: React Native with Expo (Managed Workflow)

Language: TypeScript (Strict mode enabled)

State Management: Zustand (preferred for simplicity) or Redux Toolkit. Maintain a clear separation of UI and business logic.

UI Components: React Native Paper (Material Design) or Tamagui (for performance and consistency). Alternatively, build custom, reusable components styled with StyleSheet API or a utility-first approach like twrnc. No Tailwind CSS directly in React Native.

Navigation: React Navigation

Data Visualization: react-native-svg-charts or integrate a web view with D3.js/Recharts if complex visualizations are needed.

Offline Storage: Expo FileSystem + AsyncStorage or WatermelonDB/SQLite via Expo modules for structured offline data.

OCR: Utilize a cloud-based OCR service (e.g., Google Cloud Vision, AWS Textract) via API calls, or explore Expo camera modules with potential ML Kit integration (requires research on feasibility/accuracy).

Backend:

Framework: Node.js with Express.js or NestJS (preferred for structure and TypeScript support).

Language: TypeScript

Database: PostgreSQL (for structured financial data and relational integrity). Use an ORM like Prisma (preferred) or TypeORM.

Authentication: Firebase Authentication (JWT-based).

Real-time Updates (Optional for Phase 1): Firebase Realtime Database/Firestore or WebSocket implementation (e.g., Socket.IO) for group expense updates.

Caching: Redis for frequently accessed data (e.g., user profiles, aggregated reports).

API: RESTful API.

AI Components:

Core AI: LM Studio SDK. Design clear interfaces/wrappers for interacting with the SDK. Ensure error handling and fallback mechanisms.

Food Database: Integrate with an existing API (e.g., Open Food Facts, USDA FoodData Central) or build/curate a custom database. Include nutritional info and potentially average pricing (region-dependent).

Price Comparison: Develop web scraping modules (using libraries like Cheerio/Puppeteer on the backend) targeting specific local grocery store websites/APIs (requires careful handling of terms of service and potential blocking). This is complex and might require dedicated microservices.

Infrastructure:

Hosting: Cloud platform (e.g., Vercel/Netlify for frontend if web dashboard is built, AWS/GCP/Azure for backend API, database, Redis).

CI/CD: GitHub Actions for automated testing and builds. Expo Application Services (EAS) for building and submitting mobile apps.

3. API Design Philosophy
Standard: Strictly adhere to RESTful principles (Statelessness, Cacheability, Layered System, Uniform Interface).

Documentation: Use OpenAPI (Swagger) specification. Generate documentation automatically from code annotations (e.g., using swagger-jsdoc or NestJS Swagger module).

Versioning: Implement API versioning (e.g., /api/v1/...).

Authentication: Secure all endpoints (except public ones like login/signup) using JWT middleware verifying Firebase tokens.

Request/Response: Use consistent JSON request/response formats. Implement clear error handling with standard HTTP status codes and informative error messages. Use DTOs (Data Transfer Objects) for validation and typing.

AI Consumption: Design endpoints specifically for AI interaction (e.g., /api/v1/ai/categorize-expense, /api/v1/ai/generate-recipe). These should accept structured input and return predictable, structured output.

Deployment Strategy
Environments: Maintain separate environments: development, staging, production. Use environment variables for configuration (database URLs, API keys, etc.).

Backend: Deploy the Node.js API to a scalable platform (e.g., AWS ECS/Fargate, Google Cloud Run, Heroku). Use managed services for PostgreSQL and Redis.

Frontend (Mobile App): Use Expo Application Services (EAS) Build for creating development and production builds. Use EAS Submit for distributing to TestFlight/Google Play Internal Testing and submitting to app stores. Implement Over-The-Air (OTA) updates via EAS Update for pushing JS bundle changes without requiring a full app store release.

CI/CD: Automate testing, building, and deployment using GitHub Actions.

PRs to main trigger tests.

Merges to main trigger deployment to staging.

Manual trigger or tagging releases deploys to production.

Monitoring & Logging: Integrate logging (e.g., Sentry, Datadog, AWS CloudWatch) for error tracking and performance monitoring in both frontend and backend. Set up alerts for critical errors.

This document provides the initial blueprint. Expect iteration and refinement as development progresses and challenges arise. The AI agent should prioritize clarity, adherence to standards, and robust testing throughout the process.