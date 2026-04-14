# Feature-Based Clean Architecture Guidelines

This skill enforces structural boundaries and conventions to maintain a robust, scalable Feature-Based Architecture across any software project. Whenever you are asked to design, build, or refactor components, **you must strictly adhere to these architectural principles.**

## 1. Top-Level Project Structure
- ✅ **DO** separate application source code from configuration and infrastructure metadata.
- ✅ **DO** keep deployment, CI/CD, and global configuration at the project root.
- ✅ **DO** place automated tests (end-to-end, integration) in a dedicated root-level directory.
- ❌ **DO NOT** clutter the core logic directory with environment-specific artifacts or temporary build files.

## 2. Source Code Organization (`src/` or equivalent)

### A. Features (Core Business Logic)
Features are isolated business domains (e.g., `identity_management`, `billing`, `asset_tracking`).
- **Encapsulation:** Each feature folder must contain its own entry points (Controllers/Routers), logic (Services/Use Cases), and data definitions (Models/DTOs).
- **Service-Oriented:** Implement core logic using **Class-based Services** or domain-specific modules. 
- **Inversion of Control:** Business services must not instantiate their own dependencies. Inject dependencies (Databases, External Clients, Caches) to ensure testability and decoupling.
- **Isolation:** A feature represents a vertical slice of functionality. It should not contain generic system utilities.

### B. Infrastructure (External Integrations)
Contains the implementation details of "how" the system interacts with the outside world.
- **Technology Focused:** Organized by implementation technology (e.g., `db`, `messaging`, `external_apis`, `storage`).
- **Clients & Wrappers:** Place third-party client wrappers and physical database drivers here.
- **Protocol Definitions:** If using cross-service protocols (like gRPC or GraphQL), place schemas and their generated artifacts in a structured sub-folder within Infrastructure.

### C. Common / Shared
- ✅ **DO** place generic utilities, shared constants, and framework-level helpers.
- ✅ **DO** organize constants into logical groupings (Classes or Namespaces).
- ❌ **DO NOT** place feature-specific business logic here. If logic is shared between only two features, consider creating a shared domain or refactoring the feature boundaries rather than dumping it into "Common".

## 3. Communication & Integration
- **Internal Integration:** Features should communicate via well-defined interfaces. Avoid direct access to another feature's private data storage.
- **Entry Points:** Centralize the registration of feature entry points (e.g., a main API aggregator) to keep the application bootstrap logic clean.
- **Minimal Bootstrap:** The main application entry point should only handle lifecycle events (startup/shutdown), global middleware, and routing orchestration.

## 4. Documentation & Maintenance
- Every feature should have a brief README or metadata file if it involves complex workflows or non-obvious dependencies.
- Maintain a clear separation between public interfaces and private implementation details.
