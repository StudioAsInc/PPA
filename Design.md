# Design Documentation: AI Project Planning Assistant (PPA)

## 1. System Architecture

PPA is a single-page web application (SPA) with a modern, decoupled architecture. The frontend is a React application that communicates with a Supabase backend for data persistence, authentication, and serverless functions.

### 1.1. Frontend
-   **Framework:** React with TypeScript and Vite for the build system.
-   **UI Components:** ShadCN/UI will be used for a consistent and accessible component library.
-   **Styling:** TailwindCSS for utility-first styling. The overall theme will be based on the Astro UI design.
-   **Animations:** Framer Motion for smooth and engaging user interface transitions.
-   **Icons:** Lucide-react for a clean and modern icon set.

### 1.2. Backend
-   **Platform:** Supabase will provide the core backend services.
-   **Database:** A PostgreSQL database managed by Supabase, with the schema defined in `server.txt`.
-   **Authentication:** Supabase Auth for secure user authentication, including email/password and OAuth providers (Google, GitHub).
-   **Serverless Functions:** Supabase Edge Functions will be used to securely interact with the Google Gemini API, ensuring that API keys are never exposed on the client-side.

### 1.3. AI Layer
-   **Provider:** Google Gemini API.
-   **Models:**
    -   `gemini-1.5-pro` for complex analysis and content generation.
    -   `gemini-flash` for fast, iterative prompt refinement.
-   **Interaction:** All communication with the Gemini API will be proxied through Supabase Edge Functions.

## 2. Database Schema

The database schema is designed to be simple, scalable, and secure, with Row-Level Security (RLS) enabled for all tables.

-   **`projects`:** Stores project metadata, including the project name, the persona used for AI interactions, and timestamps.
-   **`project_files`:** Holds the content of context files associated with each project.
-   **`saved_prompts`:** Stores and versions user-generated prompts for each project.

For detailed schema information, please refer to the Supabase SQL schema provided in the project's memory.

## 3. Security and Environment Setup

-   **Environment Variables:** All sensitive information, including Supabase and Gemini API keys, will be stored in a `.env.local` file and should never be committed to version control.
-   **API Key Protection:** The Gemini API key will be stored securely as a secret in Supabase and accessed only through Edge Functions.
-   **Row-Level Security (RLS):** RLS policies are enforced on all tables to ensure that users can only access their own data.
-   **Code Quality:** The project will enforce strict TypeScript type checking and ESLint rules to maintain code quality and prevent common errors.
