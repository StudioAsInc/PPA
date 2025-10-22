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
-   **Provider:** Google AI
-   **Interaction:** All communication with the Google AI APIs will be proxied through Supabase Edge Functions to ensure API keys are not exposed on the client-side.

#### Gemini Family
These are Google's most advanced and capable models. They support multimodal inputs (text, image, and audio) and have impressive reasoning and coding abilities.
-   **`gemini-2.5-pro`:** This is Google's most capable model, designed for complex reasoning, coding, and large-scale data analysis.
-   **`gemini-2.5-flash`:** This is a faster, more efficient version of the Gemini family. It features built-in tool use and a large 1 million-token context window.
-   **`gemini-2.5-flash-image`:** This model has specific optimizations for advanced image understanding and editing based on text prompts.
-   **`gemini-2.5-flash-live`:** This model is tuned for low-latency, real-time responses.
-   **`gemini-2.5-flash-tts`:** This model is for text-to-speech generation.

#### Gemma Family
These are state-of-the-art, open-weight models designed for flexibility and efficiency. They are suitable for running on laptops, desktops, or cloud infrastructure.
-   **`gemma-3-27b-it`:** This is the latest and most powerful Gemma 3 model, available in an instruction-tuned variant.
-   **`gemma-3-12b-it`:** This is an instruction-tuned Gemma model that balances performance and resource needs.
-   **`gemma-27b`:** This is a powerful version from the Gemma 2 family.
-   **`gemma-9b`:** This is a larger Gemma 2 model designed for higher-end desktops.
-   **`gemma-2b`:** This is a lightweight Gemma 2 model ideal for mobile devices.
-   **`gemma-1b`:** This is a smaller, text-only Gemma model.
-   **`codegemma`:** This is a family of models fine-tuned specifically for code completion and generation. It includes versions like `codegemma-7b` and `codegemma-2b`.
-   **`paligemma`:** This is a multimodal family of models that accepts both text and images. It includes versions like `paligemma-28b`, `paligemma-10b`, and `paligemma-3b`.

#### Generative Media Models
Google AI Studio also offers access to models for generating different types of media content, including:
-   **`Veo 3.1`:** This is Google's most advanced video generation model.
-   **`Imagen`:** This is a model for high-quality image generation.
-   **`Lyria RealTime`:** This is a model for fast audio generation.

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
