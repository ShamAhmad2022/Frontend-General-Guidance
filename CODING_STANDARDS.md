# Frontend Coding Standards & Best Practices

## Introduction

### Purpose of this document
This document outlines the coding standards, best practices, and conventions to be followed for all frontend development at our company. The goal is to ensure consistency, maintainability, and quality across our projects.

### Importance of following code standards
Adhering to code standards and best practices is crucial not only for team collaboration but also for personal growth as a developer. Consistent coding habits improve your ability to write clean, maintainable code, making it easier to debug and enhance features over time. By following these guidelines, you build a strong foundation for producing high-quality work, fostering confidence in your skills, and earning trust from your peers through reliable, readable contributions.

### Target audience
This document is intended for all team members involved in frontend development, including new developers joining the team.

### Scope
These standards apply to all frontend projects built with the following stack: Next.js, React, TypeScript, TanStack Query, Redux, Tailwind CSS, Axios, and WebSockets.

### Quick Navigation  
1. [Project Structure](#1-project-structure)  
2. [Code Style & Quality](#2-code-style--quality)  
3. [State Management](#3-state-management)  
4. [Data Fetching](#4-data-fetching)  
5. [Styling Guidelines](#5-styling-guidelines)  
6. [Internationalization (i18n)](#6-internationalization-i18n)  
7. [Asset Management](#7-asset-management)  
8. [Performance Best Practices](#8-performance-best-practices)  
9. [Git & GitHub Workflow](#9-git--github-workflow)  
10. [Recommended Libraries & Tools](#10-recommended-libraries--tools)
11. [Other Considerations](#11-other-considerations)

## 1. Project Structure

### Folder organization
Our project follows the Next.js App Router structure. Key directories include:

-   `app/`: Contains all routes and pages.
    -   `app/[locale]/`: For internationalization.
    -   `app/[locale]/(auth)/`: For authentication-related pages.
    -   `app/[locale]/(core)/`: For core application pages.
    -   `app/[locale]/(guest)/`: //provide description.
    -   `app/[locale]/(sharable)/`: For sharable pages.
    -   `app/api/`: For API routes.
-   `components/`: For shared React components.
    -   `components/forms/`: For form-related components.
    -   `components/guards/`: For route protection components.
    -   `components/shared/`: For miscellaneous shared components.
-   `lib/`: For libraries, helpers, and configurations.
    -   `lib/configs/`: For configurations like Axios and Next-Auth.
    -   `lib/constants/`: For application-wide constants.
    -   `lib/enums/`: For enums and project Routes and backend Endpoint.
    -   `lib/hooks/`: For custom React hooks.
    -   `lib/locales/`: For handling localization.
    -   `lib/providers/`: For React context providers.
    -   `lib/schemas/`: For Zod validation schemas.
    -   `lib/store/`: For Redux Toolkit store setup.
    -   `lib/types/`: For TypeScript type definitions.
    -   `lib/style/`: for CSS and custom styles.
    -   `lib/utils/`: For utility and helper functions.
-   `public/`: For static assets like images and fonts.
    -   `public/images/`: It can be splitted further based on the project, ex: svg/ png/ auth/ core/ etc..
    -   `public/fonts/`: fonts.

### Naming conventions
- **Components:** PascalCase (e.g., MyComponent.tsx)
- **Functions/Variables:** camelCase (e.g., myFunction, myVariable)
- **Files:** kebab-case for pages and routes (e.g., my-page/page.tsx), PascalCase for components.
- **Folders:** kebab-case (e.g., login-form/, user-profile/)
- **Hooks:** use prefix (e.g., useCustomHook.ts)
- **Types & Interfaces:** PascalCase (e.g., User, AuthPayload, UserProfileProps)
- **Constants:** SCREAMING_SNAKE_CASE (e.g., API_BASE_URL, MAX_RETRY_COUNT)

### Guidelines on file and component sizes
-   **One component per file:** Each React component should be in its own file.
-   **Keep components small:** Aim for components to be around 250-300 lines of code. If a component grows too large, consider breaking it down into smaller, more manageable components.

## 2. Code Style & Quality

### TypeScript best practices
-   **Strict mode:** Our `tsconfig.json` has `"strict": true` enabled. Adhere to strict type-checking rules.
-   **Avoid `any`:** Do not use the `any` type. If a type is unknown, use `unknown` and perform type-checking.
-   **Use enums and types:** Use TypeScript `enum` for sets of named constants and `type` or `interface` for defining object shapes.
-   **Path aliases:** Use `@/*` for absolute imports from the project root.

### React patterns
-   **Functional components only:** All new components should be functional components using React Hooks.
-   **Hooks-first approach:** Leverage React Hooks for state management, side effects, and context.

### ESLint rules overview
We use ESLint with `next/core-web-vitals` and `@typescript-eslint/recommended`. Key rules are defined in `.eslintrc.cjs`. Please ensure your editor is configured to show ESLint errors and warnings.

### Prettier formatting rules
Code formatting is handled by Prettier. Our configuration (`.prettierrc`) enforces:
-   `printWidth`: 100
-   `tabWidth`: 4
-   `singleQuote`: false
-   `semi`: true
-   `trailingComma`: "all"

Please configure your editor to format on save.

### VS Code recommended settings / extensions
-   ESLint (`dbaeumer.vscode-eslint`)
-   Prettier - Code formatter (`esbenp.prettier-vscode`)
-   Tailwind CSS IntelliSense (`bradlc.vscode-tailwindcss`)

## 3. State Management

### When to use Redux vs. local state or TanStack Query
-   **Local State (`useState`, `useReducer`):** For component-specific state that doesn't need to be shared.
-   **TanStack Query:** For managing server state (fetching, caching, updating data).
-   **Redux:** For global client state that needs to be shared across many components (e.g., user authentication status, theme).

### Folder structure for Redux slices
Redux slices are located in `lib/store/`. Each slice should have its own file (e.g., `auth.ts`, `core.ts`).

### Naming conventions for state and actions
Follow the standard Redux Toolkit conventions for creating slices, actions, and reducers.

### Use of middleware
We use Redux Toolkit, which includes `redux-thunk` by default for async actions.

## 4. Data Fetching

### Axios setup
An Axios instance is configured in `lib/configs/axios/client.ts`. This instance should be used for all HTTP requests. Interceptors can be added here for handling things like authentication tokens.

### Usage of TanStack Query
-   **Query Keys:** Use descriptive and unique query keys. A good practice is to use an array with the entity name and any parameters (if needed) (e.g., `['patients', patientId]`).
-   **Caching Strategy:** Rely on TanStack Query's default caching strategy. Configure `staleTime` and `cacheTime` as needed for specific queries.

### When to use WebSockets
Use WebSockets for features that require real-time, bidirectional communication, such as live notifications or chat.

## 5. Styling Guidelines

### Tailwind CSS usage rules
-   **No inline styles:** Avoid using the `style` attribute on components. Use Tailwind utility classes instead.
-   **Consistent spacing:** Use the spacing values defined in the Tailwind theme (padding, margin, width, etc..).

### Use of utility classes vs. component extraction (@apply)
Prefer using utility classes directly in your JSX. Use `@apply` sparingly, and only for extracting common component styles into a CSS file when necessary.

### Custom theme usage
Our custom theme is defined in `tailwind.config.ts`. It includes custom colors, screens, and other theme values. Always use these theme values to maintain consistency.

## 6. Internationalization (i18n)

### Tool used
We use a custom i18n solution built into the Next.js app structure, located in `lib/locales/`.

### Folder structure for translations
Translation files are located in `lib/locales/` (`en.ts` and `ar.ts`).

### Rules for dynamic translation keys
Avoid constructing translation keys dynamically at runtime.

### Avoiding hardcoded strings
All user-facing strings must be added to the translation files and accessed via the i18n hooks/helpers.

## 7. Asset Management

### Image optimization
Use the `next/image` component for all images to get automatic optimization. Prefer SVG for icons and logos where possible.

### Icon libraries
We use `@iconify/react` for icons.

### File naming and folder organization
Organize assets logically within the `public/` directory.

## 8. Performance Best Practices

### Lazy loading
-   **Components:** Use `next/dynamic` to lazy-load components that are not needed on the initial page load.
-   **Images:** The `next/image` component handles lazy loading of images by default.

### Debouncing/throttling
Use libraries like `use-debounce` for expensive operations that are triggered by frequent events (e.g. search input).

### Memoization
Use `React.memo`, `useMemo`, and `useCallback` to prevent unnecessary re-renders, but only after profiling and identifying performance bottlenecks.

## 9. Git & GitHub Workflow

### Branching strategy
-   `main`: Production-ready code.
-   `develop`: Integration branch for features.
-   `bugfix/...`: For bug fixes.

### Commit message style
Write clear, concise, and descriptive commit messages that summarize the changes made in the present tense, e.g., "Enable lazy loading for images to improve performance."

### PR process
-   All PRs must be reviewed and approved by the leader.
-   PRs should have a clear description of the changes.
-   Ensure all CI checks are passing before merging.

## 10. Recommended Libraries & Tools

### Libraries for consistency
-   `zod`: For schema validation.
-   `react-hook-form`: For managing forms.
-   `clsx`: For conditionally joining class names (or you can use `cn` from HeroUI).

### Developer tools
-   React DevTools
-   Redux DevTools
-   Tanstack Devtools (ReactQuery Devtools)
-   VSCode extensions mentioned in section 2.

## 11. Other Considerations

- Remove `console.log` statements before deploying:
  Debug logs can clutter the browser console, reveal internal data, and affect performance. Clean them up to maintain a polished production environment.

- Use semantic HTML tags:
  Semantic elements like `<header>`, `<main>`, `<section>`, and `<footer>` enhance accessibility, improve SEO, and make your markup more meaningful and maintainable.

- Use unique keys when rendering lists:
  Avoid using only the index as a key when mapping over long or dynamic arrays. Instead, combine it with a unique identifier (like an ID) to ensure consistent rendering and prevent UI glitches.