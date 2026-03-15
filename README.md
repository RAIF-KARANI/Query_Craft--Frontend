# QueryCraft Frontend

## Overview

QueryCraft Frontend is the user interface for the QueryCraft application, an AI-driven database querying assistant. Built with Next.js 15 and React 19, it provides a highly interactive, responsive, and visually engaging chat-based interface. Users can interact with Large Language Models to generate database queries, visualize code with syntax highlighting, import database files, and manage their chat sessions.

> **Note**: This repository contains the frontend client code. It requires the backend API to function. The backend application can be found here: [QueryCraft Backend]([https://github.com/RAIF-KARANI/Query_Craft--Backend]).

## Key Features

* **Interactive Chat Interface**: Real-time chat UI featuring typing indicators, message history, and structured rendering of AI responses (`ChatWindow`, `ChatMessage`, `ChatInput`).
* **Code & Query Visualization**: Beautifully formatted code blocks with syntax highlighting powered by PrismJS (`CodeCard.tsx`).
* **Immersive 3D Elements**: Integrates WebGL 3D rendering using Three.js and React Three Fiber/Drei for engaging landing or introductory visuals.
* **Database Import Management**: Dedicated dialogs for users to upload and manage local database files (CSV, JSON, SQLite) directly from the UI (`DatabaseImportDialog.tsx`).
* **Authentication Flow**: Built-in authentication handling, auto-login hooks, and protected route management (`AuthPage.tsx`, `AuthProviderClient.tsx`, `useAutoLogin.ts`).
* **Theming & Accessibility**: Fully accessible components built on Radix UI, styled with Tailwind CSS, supporting seamless Dark/Light mode switching (`next-themes`).
* **Toast Notifications**: Elegant, non-intrusive state and error notifications using Sonner.

## Architecture / System Design

The application utilizes the modern Next.js App Router (`src/app/`) paradigm for server-side rendering and client-side routing. 
* **Component Strategy**: It strictly separates pages/views (`src/components/pages/`), domain-specific features (`src/components/chat/`, `src/components/auth/`), and reusable UI primitives (`src/components/ui/` based on shadcn/ui).
* **State & Data Fetching**: Relies on React hooks for local state and client-side API communication with the QueryCraft Backend REST API.
* **Styling**: Tailwind CSS v4 is used for utility-first styling, combined with Framer Motion for fluid layout animations and transitions.

## Tech Stack

* **Framework**: Next.js 15.5.7
* **Library**: React 19.1.0 (with React DOM)
* **Language**: TypeScript
* **Styling & UI**: Tailwind CSS, Radix UI Primitives, `tailwind-merge`, `tailwindcss-animate`
* **Animations & 3D**: Framer Motion, Three.js, `@react-three/fiber`, `@react-three/drei`
* **Utilities**: PrismJS (syntax highlighting), Sonner (toast notifications), `next-themes` (theme management)

## Project Structure

```text
Query_Craft--Frontend/
├── package.json                   # Dependencies and build scripts
├── next.config.ts                 # Next.js configuration
├── tailwind.config.ts             # Tailwind CSS configuration
├── postcss.config.mjs             # PostCSS processing setup
├── public/                        # Static assets (SVGs, images, fonts)
└── src/
    ├── app/                       # Next.js App Router (layout.tsx, page.tsx, globals.css)
    ├── components/
    │   ├── auth/                  # Authentication providers and client logic
    │   ├── chat/                  # Chat interface elements (Header, Input, Message, Window, CodeCard)
    │   ├── layout/                # Global layout elements (Sidebar, Header, Mobile Triggers)
    │   ├── modals/                # Dialog windows (DatabaseImportDialog, SettingsDialog)
    │   ├── pages/                 # Top-level page components (AuthPage, ChatApp, IntroPage)
    │   └── ui/                    # Reusable Radix UI/shadcn components (buttons, dialogs, inputs, etc.)
    ├── hooks/                     # Custom React hooks (e.g., useAutoLogin.ts)
    ├── lib/                       # Utility functions (e.g., utils.ts for Tailwind class merging)
    └── types/                     # TypeScript declaration files (PrismJS, React-Three)
```

## Installation

Run the following commands to clone the repository, navigate to the directory, and install the necessary dependencies.

```bash
# Clone the repository
git clone https://github.com/RAIF-KARANI/Query_Craft--Frontend.git

# Navigate into the project directory
cd Query_Craft--Frontend

# Install NPM dependencies
npm install
```

## Configuration

The frontend needs to know where the backend API is hosted. Create a `.env.local` file in the root directory and specify the API URL.

```bash
cat <<EOT >> .env.local
# Backend API URL (Update if your backend is hosted elsewhere)
NEXT_PUBLIC_API_URL=http://localhost:5001/api
EOT
```

(Note: Ensure your backend CORS configuration permits requests from the frontend's origin).

## Usage

### Development Mode

Runs the app in development mode on http://localhost:3000.

```bash
npm run dev
```

### Production Build

Builds the application for production usage.

```bash
npm run build
npm run start
```

## Security Notes

* **Client-Side Auth**: JWT tokens handled by `AuthProviderClient.tsx` and `useAutoLogin.ts` should be stored securely (preferably HTTP-only cookies, or handled carefully if in localStorage/sessionStorage to mitigate XSS risks).
* **Sanitization**: Code blocks and AI-generated messages rendered via PrismJS and the chat UI should escape HTML characters to prevent cross-site scripting (XSS) attacks.

## Limitations

* 3D rendering elements (Three.js) may cause higher GPU/CPU utilization on lower-end devices.
* Requires an active, running instance of the QueryCraft Backend to function; it is not a standalone client app.

## Future Improvements

* Implement WebSocket connections for true streaming of LLM responses (rather than waiting for full JSON payload completion).
* Add detailed error boundaries for the 3D canvas elements to prevent app crashes on unsupported browsers.
* Integrate extensive end-to-end (E2E) testing using Playwright or Cypress.

## License

This project is licensed under the MIT License - see the LICENSE file for details.
