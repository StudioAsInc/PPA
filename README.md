# AI Project Planning Assistant (PPA)

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)

An AI-powered project planning assistant to help developers create pre-production plans for any project. PPA streamlines the process of brainstorming, planning, and generating high-quality prompts for AI coding agents.

## 📚 Table of Contents

- [🧠 Core Concept](#-core-concept)
- [🧩 Tech Stack](#-tech-stack)
- [📦 Core Features](#-core-features)
- [🚀 Getting Started](#-getting-started)
- [📄 License](#-license)
- [©️ Copyright](#️-copyright)
- [🤔 FAQs](#-faqs)

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

This project is licensed under the GNU General Public License v3.0. See the [LICENSE](LICENSE) file for details.

## ©️ Copyright

© 2025, StudioAs Inc.
Owned by: MD. ASHIK AHMED
GitHub: [@TheRealAshik](https://github.com/TheRealAshik)
Email: [mashikahamed0@gmail.com](mailto:mashikahamed0@gmail.com)

## 🤔 FAQs

**1. What is the main purpose of the AI Project Planning Assistant (PPA)?**

> PPA is designed to help software developers plan complex projects by providing a structured environment for brainstorming, managing project context, and refining prompts for AI coding agents. It acts as a bridge between human developers and AI, streamlining the pre-production phase of software development.

**2. What is the technology stack used in this project?**

> The frontend is built with React, TypeScript, Vite, TailwindCSS, and ShadCN/UI. The backend is powered by Supabase, using its PostgreSQL database, authentication, and serverless functions. The AI layer integrates with Google's Gemini and Gemma models.

**3. Is this project open source?**

> Yes, PPA is licensed under the GNU General Public License v3.0 (GPLv3). You are free to use, modify, and distribute the software under the terms of the license.

**4. How do I get started with the project?**

> To get started, you will need to clone the repository, install the dependencies, and set up your environment variables, including your Supabase and Google AI API keys. For detailed instructions, please refer to the [Getting Started](#-getting-started) section of this README.
