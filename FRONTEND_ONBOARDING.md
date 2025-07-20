# Frontend Development Onboarding Guide

Welcome to the team! This guide will help you get up to speed with our frontend development process. Our projects are primarily built using Next.js and Vite with React, so this document will provide you with the essential information to get started.

### Quick Navigation
1. [Getting Started](#getting-started)
2. [Project Structure](#project-structure)
3. [Main Packages & Libraries](#main-packages--libraries)
4. [Hooks & Patterns](#hooks--patterns)
5. [Shared, reusable and Custom Code](#shared-reusable-and-custom-code)
6. [Others](#others)

## Getting Started

Follow these steps to set up your local development environment:

1.  **Clone the repository:**
    ```bash
    git clone REPOSITORY_LINK
    ```
2.  **Install dependencies:**
    ```bash
    npm install
    ```
3.  **Set up environment variables:**
    Create a `.env.local` if it's a Nextjs app (or just `.env` if it's a Vite React app) file in the root of the project and add the necessary environment variables. You can use the following template as a starting point:
    ```
    # Add your environment variables here
    ```
4.  **Run the development server:**
    ```bash
    npm run dev
    ```
    The application will be available at `http://localhost:3000` if it's a Nextjs app, or `http://localhost:5173` if it's a Vite React app.

## Project Structure

Our Next.js application follows a standard structure. Here's an overview of the main directories:

- `app/`: This is the main directory for our application. It contains all of our routes, pages, and layouts.
  1. `app/[locale]/`: This directory contains all of our internationalized routes. The `[locale]` segment is used to determine the language of the application, and can be splitted into the following:
  - `app/[locale]/`: For internationalization.
  - `app/[locale]/(auth)/`: For authentication-related pages.
  - `app/[locale]/(core)/`: For core application pages.
  - `app/[locale]/(guest)/`: For pages accessible to unauthenticated (guest) users.
  - `app/[locale]/(sharable)/`: For sharable pages.
  2. `app/api/`: This directory contains all of our API routes.
- `components/`: This directory contains all of our reusable React components and can be splitted to the following:
  - `components/forms/`: For form-related components.
  - `components/guards/`: For route protection components.
  - `components/shared/`: For shared components.
- `lib/`: This directory contains all of our shared code, including hooks, utility functions, and constants, and can be splitted to the following:
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
- `public/`: This directory contains all of our static assets, such as images and fonts.

## Main Packages & Libraries

We use a variety of external libraries to help us build our application. Here are some of the most important ones:

- **TypeScript:** A typed superset of JavaScript that compiles to plain JavaScript.
- **TanStack Query:** A data-fetching library that helps us manage server state.
- **Redux:** A predictable state container for JavaScript apps.
- **Tailwind CSS:** A utility-first CSS framework for rapidly building custom designs.
- **HeroUI:** A React UI library for building beautiful and accessible user interfaces.
- **Axios:** A promise-based HTTP client for the browser and Node.js.
- **NextAuth.js:** An authentication library for Next.js applications.
- **Zod:** A TypeScript-first schema declaration and validation library, used along with useForm hook.
- **useForm hook:** A hook for managing form state and validation.
- **Iconify:** A library for using icons.

## Hooks & Patterns

We use a number of custom hooks to encapsulate and reuse logic throughout our application. Here are some of the most important ones:

### `useLocale`

This hook is used to manage internationalization and navigation. It returns the following properties:

- `locale`: The current locale (e.g., `en` or `ar`).
- `toggleLocale`: A function to switch between locales.
- `t`: An object containing all of the translations for the current locale.
- `navigate`: A function to navigate to a new page.
- `currentRout`: The current route.


### `useUploadFile`

This hook is used to manage file uploads. It returns the following properties:

- `onInputChange`: A function to handle the `onChange` event of the file input.
- `InputComponent`: A component that renders a file input.
- `file`: The file that was selected by the user.
- `view`: A data URL of the selected file.
- `setFile`: A function to manually set the file.

### `useChatRoomSocket` & `useRoomsSocket`

These hooks are used to manage our WebSocket connections for real-time chat features. They handle connecting to the server, sending and receiving messages, and managing the state of the chat rooms.

## Shared, reusable and Custom Code

We have a number of reusable components and utility functions that you should be aware of.

### Reusable Components

You can find our reusable components in the `components` directory at the root. Some of the most important ones include:

- `SharedText`: A component for displaying text with different variants.
- `LoadingSpinner`: A component for displaying a loading spinner.
- `MainButton`: A primary button for main actions.
- `SecondaryButton`: A secondary button for alternative actions.
- `SharedModal`: A sharable modal with different properties.

### Utility Functions

You can find our utility functions in the `lib/utils` directory. Some of the most important ones include:

- `isRTL`: A function to check if the current locale is right-to-left.
- `stringHelpers`: A set of functions for working with strings.
- `date-format`: A set of functions for working with and reformatting date and time.

## Others

### Development Environment Tips

**Linting and Formatting:** We use ESLint and Prettier to enforce a consistent code style. You can run the following commands to lint and format your code:
  ```bash
  npm run lint
  npm run format
  ```
### Starting a new project
To save time on setup and package installation, it is recommended to clone a template from the following repository when starting a new project: [https://github.com/ShamAhmad2022/nextjs-app-template](https://github.com/ShamAhmad2022/nextjs-app-template)

### Coding Standards & Best Practices
It is recommended to have a look at the following to have a general idea of the coding standards and best practices that we follow: [https://github.com/ShamAhmad2022/Frontend-General-Guidance/blob/main/CODING_STANDARDS.md](https://github.com/ShamAhmad2022/Frontend-General-Guidance/blob/main/CODING_STANDARDS.md)
