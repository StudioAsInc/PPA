# AI Project Planning Assistant (PPA)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

An AI-powered project planning assistant to help developers create pre-production plans for any project. PPA streamlines the process of brainstorming, planning, and generating high-quality prompts for AI coding agents.

## 🧠 Core Concept

PPA acts as a bridge between human developers and AI coding assistants. It manages project context, stores files and prompts securely in Supabase, and uses Google's AI models for:

-   Brainstorming project ideas & features
-   Generating structured project plans
-   Refining prompts iteratively
-   Managing prompt templates for AI agents

## 🧩 Tech Stack

### Frontend

-   **Framework:** React with TypeScript
-   **Build Tool:** Vite
-   **Styling:** TailwindCSS
-   **UI Components:** ShadCN/UI
-   **Animations:** Framer Motion
-   **Icons:** Lucide-react

### Backend

-   **Platform:** Supabase
-   **Database:** PostgreSQL
-   **Authentication:** Supabase Auth
-   **Serverless Functions:** Supabase Edge Functions

### AI Layer

-   **Provider:** Google AI
-   **Models:** Gemini and Gemma families

## 📦 Core Features

-   **Authentication & Onboarding:** Secure user authentication with Supabase, including OAuth for Google and GitHub.
-   **Project Management:** CRUD operations for projects, with context file management.
-   **Prompt Studio:** A centralized editor for writing, refining, and versioning prompts.
-   **AI Project Brainstorming:** Generate project ideas, feature backlogs, and roadmaps with AI.
-   **Prompt Refinement System:** Iteratively improve prompts with AI suggestions and a diff viewer.

## 🚀 Getting Started

### Prerequisites

-   Node.js (v18 or later)
-   npm, pnpm, or yarn
-   A Supabase account
-   A Google AI API key

### Installation

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/your-username/ppa.git
    cd ppa
    ```

2.  **Install dependencies:**
    ```bash
    npm install
    ```

3.  **Set up environment variables:**
    -   Create a `.env.local` file in the root of the project.
    -   Add your Supabase URL, anon key, and Google AI API key:
        ```
        SUPABASE_URL="your-supabase-url"
        SUPABASE_ANON_KEY="your-supabase-anon-key"
        GEMINI_API_KEY="your-google-ai-api-key"
        ```

4.  **Run the development server:**
    ```bash
    npm run dev
    ```

## 📄 License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
