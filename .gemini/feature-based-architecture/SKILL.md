# Feature-Based Clean Architecture Guidelines

This skill enforces the structural boundaries and conventions for the Main Orchestrator service to maintain a robust, scalable Feature-Based Architecture. Whenever you are asked to create new features or refactor code in this service, **you must strictly adhere to the following rules.**

## 1. Top-Level Project Structure
- ✅ **DO** place only application code inside the `src/` directory.
- ✅ **DO** keep deployment, configuration, and testing infrastructure at the project root.
  - `tests/`: End-to-end and unit tests.
  - `migrations/`: Alembic migrations configuration and revisions.
  - `pytest.ini`, `alembic.ini`, `.env`, `docker-compose.yml`, etc.
- ❌ **DO NOT** place `tests` or `migrations` inside `src/`.

## 2. Source Code Organization (`src/`)

### `src/features/` (Core Business Logic)
Features are isolated business domains (e.g., `user_management`, `face_recognition`, `camera_management`).
- **Cohesion:** Each feature folder must contain its own `router.py`, `service.py`, `models.py`, and `schemas.py`.
- **Services:** Logic must be implemented using **Class-based Services** (e.g., `FaceRecognitionService`). 
- **Dependency Injection:** Routers must inject dependencies (Database Session, Redis Client, external clients) into the Service constructors via dependency factories. Do not perform direct database queries directly in routers.
- **Isolation:** A feature should not contain generic system utilities or infrastructure setup logic.

### `src/infra/` (Infrastructure & Third-Party Integrations)
Contains connections to the outside world, external services, and databases.
- Organized by technology: `infra/database/session.py`, `infra/redis/client.py`, `infra/websocket/manager.py`.
- **gRPC Architecture:** 
  - `.proto` files reside in `infra/grpc/proto/`.
  - Generated code (`*_pb2.py`) resides in `infra/grpc/generated/`.
  - Client wrappers (`FaceAIClient`) reside in integration-specific folders (e.g., `infra/face_ai/client.py`) and import from `infra/grpc/generated/`.

### `src/common/` (Shared Utilities)
- ✅ **DO** place generic utilities (`utils.py`) and constants (`constants.py`).
- ✅ **DO** organize constants into Classes (e.g., `RedisConstants`, `ServiceConstants`) instead of global variables.
- ❌ **DO NOT** place feature-specific business logic (e.g. deduplication logic for face detection) in the common folder. Business logic belongs inside its specific feature service.

## 3. API Aggregation
- Place individual routers in their respective `src/features/[feature_name]/router.py`.
- Centralize and include all individual routers in `src/api.py`.
- `src/main.py` simply mounts `src/api.py` and handles the application lifespan (startup/shutdown scripts) and top-level middleware. Keep `main.py` clean and minimal.
