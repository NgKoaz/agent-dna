# React Feature-Based Architecture Guidelines

This skill enforces structural boundaries and conventions to maintain a robust, scalable Feature-Based Architecture across React/UmiJS projects. Whenever you are asked to design, build, or refactor React components or modules, **you must strictly adhere to these architectural principles.**

## 1. Top-Level Directory Structure
- ✅ **DO** separate application configuration, routing, and global assets from the core feature logic.
- ✅ **DO** group code by **Feature (Domain)** rather than by technical type (e.g., placing all components together, all hooks together is an anti-pattern here).
- ❌ **DO NOT** create a giant `components/` or `hooks/` folder at the root of `src/`.

### Standard Layout Example (UmiJS context)
```text
src/
├── layouts/                     # Global/Outer wrappers (Sidebar, TopBar)
├── pages/                       # Feature modules (Route-based)
│   ├── monitor/                 # Feature A
│   ├── identities/              # Feature B
│   └── settings/                # Feature C
├── shared/                      # Code utilized by ≥ 2 features
└── app.ts                       # App runtime config
```

## 2. Feature Isolation (`src/pages/[feature]/`)
Each feature represents an isolated business domain or major route module.
- **Encapsulation:** A feature folder must contain its own UI `components/`, custom `hooks/`, data fetching `services/`, and the main route `index.tsx`.
- **High Cohesion, Low Coupling:** Everything needed to render and operate that feature should live inside its directory. Deleting a feature folder should cleanly remove its functionality without breaking other features (excluding navigation links).
- **Sub-routing:** If a feature has sub-routes (e.g., `identities/enroll`), organize them as nested feature directories if they possess distinct logic, or keep them lightweight within the parent feature.

## 3. The Shared Directory (`src/shared/`)
This is the strict isolation zone for reusable code.
- **Rule of Two:** Only promote components, hooks, or utilities to `src/shared/` if they are explicitly used by **two or more** different features.
- ✅ **DO** place atomic UI components (like `StatusBadge`, `ActionModal`), global models (state management), and global constants here.
- ❌ **DO NOT** place feature-specific business logic in `shared/`. If logic is heavily tied to a single feature domain, it belongs in that feature's directory.

## 4. State Management & Data Fetching
- **Local State:** Use React's built-in `useState` and `useReducer` for UI state within components.
- **Feature State / API:** Use data fetching libraries (like `useRequest` from ahooks/Umi, React Query, or SWR) directly within the feature's `hooks/` or `index.tsx` to handle server state, caching, and loading indicators.
- **Global / Shared State:** For global streams (e.g., WebSockets, Theme, User Auth), use framework-level global stores (like Umi's `@umijs/max` models, Zustand, or Redux) placed under `src/shared/models/`.

## 5. Dependency Rules
1. **Feature to Feature:** ❌ A feature should **never** import from another feature's private directory.
2. **Feature to Shared:** ✅ Features can import freely from `src/shared/`.
3. **Shared to Feature:** ❌ `shared/` must **never** import from inside a feature.
4. **Layout to Feature:** ❌ Layouts should act as shells. They shouldn't be tightly coupled to the inner workings of specific features.

## 6. Naming Conventions & Styling
- Component Files: `PascalCase.tsx` (e.g., `CameraCard.tsx`).
- Hooks Files: `camelCase.ts` (e.g., `useCameraStatus.ts`).
- Service Files: `[domain]Api.ts` or `services.ts` (e.g., `enrollmentApi.ts`).
- Styling: Use Module CSS (`styles.module.css`), Styled Components, or Tailwind. Ensure styles are scoped to avoid global collisions.
