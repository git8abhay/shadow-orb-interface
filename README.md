# 🌑 Shadow Assistant & Orb Interface
### *Next-Generation AI Recruitment & Assessment Ecosystem*

![Build Status](https://img.shields.io/badge/build-passing-brightgreen)
![Tech Stack](https://img.shields.io/badge/stack-Spring_Boot_|_React_|_OpenAI-blueviolet)
![License](https://img.shields.io/badge/license-MIT-blue)
![Version](https://img.shields.io/badge/version-1.0.0--beta-orange)

---

## 📖 Executive Summary

**Shadow Assistant** is an enterprise-grade recruitment platform designed to mitigate hiring bias and automate technical screening through **Generative AI** and **Retrieval-Augmented Generation (RAG)**.

The system features a **Microservices-ready Backend (Spring Boot)** and a **Reactive Frontend (React/Vite)** that facilitate a dual-role workflow:
1.  **Candidate Copilot:** Empowering applicants with AI-driven resume parsing, auto-matching, and an **Anti-Cheat AI Interview Environment**.
2.  **Recruiter Command Center:** Providing Talent Acquisition teams with semantic search capabilities, **real-time bias analytics**, and automated technical depth assessment.

---

## 🏗️ System Architecture

The application implements a **Stateless, Decoupled Architecture** ensuring scalability and security.

### 🔌 Backend: Shadow Assistant (Spring Boot)
* **Core Framework:** Spring Boot 3.x with Spring Security 6.
* **AI Orchestration:** **Spring AI** framework integrating **OpenAI GPT-4o** and **Whisper** models.
* **RAG Pipeline:**
    * **Ingestion:** Apache PDFBox for high-fidelity text extraction from Resumes and Job Descriptions (JDs).
    * **Vectorization:** Implementation of `SimpleVectorStore` (extensible to PgVector/Pinecone) to generate high-dimensional embeddings.
    * **Semantic Retrieval:** Context-aware matching of Candidate profiles against JDs using cosine similarity.
* **Security Layer:**
    * **Dual-Token Authentication:** Short-lived JWT Access Tokens combined with **HttpOnly, Secure, SameSite=Strict** Refresh Token cookies to prevent XSS/CSRF attacks.
    * **RBAC (Role-Based Access Control):** Granular authorization logic for `CANDIDATE` and `RECRUITER` roles.

### 💻 Frontend: Shadow Orb Interface (React)
* **Runtime:** Vite + React 18 + TypeScript for type-safe, high-performance rendering.
* **State Management:** `React Query` (@tanstack/query) for server-state synchronization and optimistic updates, alongside `Context API` for global auth state.
* **UI/UX System:** **Shadcn/UI** (Radix Primitives) coupled with **Tailwind CSS** for a responsive "Glassmorphism" aesthetic.
* **Interactive Analytics:** **Recharts** for data visualization (Hiring Funnels, Radar Charts).
* **Motion Engineering:** **Framer Motion** for fluid layout transitions and micro-interactions.

---

## 🚀 Key Functional Modules

### 1. Intelligent Document Processing (IDP) & RAG
The system moves beyond keyword matching by implementing a **Vector-based Semantic Search Engine**.
* **Resume Vectorization:** Resumes are parsed, cleaned via LLM prompts (removing PII/irrelevant data), chunked, and embedded into the vector store.
* **Contextual Matching:** The "Eliminator" service retrieves candidate vectors relevant to specific JD vectors, enabling **concept-based matching** (e.g., matching "Flask" to "Python Backend" even if explicit keywords are missing).

### 2. Autonomous Audio Interview Engine
A fully automated, secure interview environment designed to assess technical depth.
* **Speech-to-Text Pipeline:** Utilizing **OpenAI Whisper** with `temperature=0` for deterministic, high-accuracy transcription of candidate responses.
* **Depth Analysis:** A custom "Depth Detector" prompt analyzes transcripts to differentiate between shallow memorization and deep conceptual understanding.
* **Anti-Cheat Heuristics:** The frontend leverages the **Page Visibility API** and **Fullscreen API** to detect tab switching or window exits, flagging integrity violations in real-time.

### 3. Bias Detection & Ethics Engine
* **Algorithmic Auditing:** The `BiasAnalytics` module aggregates scoring data to visualize disparities across demographic axes (Gender, Age, Ethnicity).
* **Diversity Radar:** Real-time visualization of candidate pool diversity metrics.
* **Fairness Insights:** AI-generated textual analysis recommending actionable steps to reduce bias (e.g., blinding institution names).

---

## 🛠️ Technology Stack

| Domain | Technology | Purpose |
| :--- | :--- | :--- |
| **Backend** | **Java 17 / Spring Boot 3** | Core Application Logic |
| **AI / LLM** | **Spring AI / OpenAI GPT-4o** | Reasoning, Summarization, RAG |
| **Audio** | **OpenAI Whisper** | Speech-to-Text Transcription |
| **Database** | **PostgreSQL** | Relational Data & Vector Storage |
| **Frontend** | **React / TypeScript / Vite** | Client-Side Application |
| **Styling** | **Tailwind CSS / Shadcn UI** | Component Design System |
| **Security** | **Spring Security / JWT** | AuthN & AuthZ |
| **Docs** | **PDFBox** | Document Parsing |

---

## 📦 Installation & Setup

### Prerequisites
* Java JDK 17+
* Node.js v18+ & npm
* PostgreSQL Instance
* OpenAI API Key

### Backend Setup
1.  **Configure Environment:**
    Update `src/main/resources/application.yaml`:
    ```yaml
    spring:
      datasource:
        url: jdbc:postgresql://localhost:5432/shadow_db
        username: <DB_USER>
        password: <DB_PASS>
      ai:
        openai:
          api-key: <OPENAI_API_KEY>
    ```
2.  **Build & Run:**
    ```bash
    ./mvnw clean install
    ./mvnw spring-boot:run
    ```

### Frontend Setup
1.  **Install Dependencies:**
    ```bash
    cd shadow-orb-interface
    npm install
    ```
2.  **Environment Variables:**
    Create `.env`:
    ```env
    VITE_API_URL=http://localhost:8090/api
    ```
3.  **Launch Development Server:**
    ```bash
    npm run dev
    ```

---

## 🔐 Security Protocols

* **CSRF Protection:** Stateless session management mitigates CSRF risks.
* **Input Sanitization:** All file uploads are processed via streams; filenames are sanitized.
* **Secure Headers:** Application enforces rigorous CORS policies allowing only trusted origins.

---

## 🤝 Contribution

We welcome architectural improvements and feature extensions. Please adhere to **Conventional Commits** standards when submitting Pull Requests.

1.  Fork the repository
2.  Create your feature branch (`git checkout -b feature/NeuralMatching`)
3.  Commit your changes (`git commit -m 'feat: Implement LSTM based matching'`)
4.  Push to the branch (`git push origin feature/NeuralMatching`)
5.  Open a Pull Request

---

### *Engineered for the Future of Work.*
