# MBTQ.dev – Deaf-First Innovation Ecosystem

### 🚀 Status: Foundation Built, Backend Integration in Progress

MBTQ.dev is a **Deaf-First ecosystem** built to empower entrepreneurs, researchers, and creators with AI-driven, accessible business tools. It is designed around the **Idea → Build → Grow → Managed** lifecycle and powered by **MagicianCore** and the **360Magicians** suite.

---

## 🌐 Ecosystem Overview

* **MBTQ.dev Frontend (Pinkflow UI)**

  * React + TypeScript SPA
  * Role-based UI (Developer, Researcher, Contributor)
  * Component-driven architecture
  * Mocked backend services (ready for API swap-in)
  * Gemini API integration (to be proxied securely via backend)

* **MBTQ FastAPI Backend (Scaffolded)**

  * Modular services:

    * **DeafAuth** (Identity & Authentication)
    * **PinkSync** (Real-time sync & notifications)
    * **FibonRose** (Trust & Ethics Engine)
    * **360Magicians** (AI Business Agents)
  * SQLAlchemy models for unified schema
  * API routers & placeholder services
  * JSON schema contract (`build.json`)

* **PinkSync Node.js Service**

  * WebSocket backbone for real-time collaboration
  * Powers Pinkflow multi-user workspace

* **MagicianCore Agents**

  * AI-driven service agents handling lifecycle: Idea → Build → Grow → Managed
  * Connected to `business-magician-api`

---

## 📌 Current Frontend State

✅ Feature-complete for MVP scope
✅ Mocked services allow testing without backend
✅ Role-based components functional
✅ Ready for backend API integration

Next step: Replace mocked data with live API calls.

---

## 📌 Backend API Tasks

1. **Authentication API**

   * `POST /api/auth/login` → JWT + User object
   * `POST /api/auth/logout` → Invalidate session
   * `GET /api/auth/user` → Return current profile
   * `POST /api/user/profile/sync` → Sync FibonRose trust profile

2. **Workspace API**

   * `GET /api/workspace/tree` → File structure
   * `GET /api/workspace/file?path=` → File content
   * `PUT /api/workspace/file?path=` → Update file
   * `POST /api/workspace/file` → Create file
   * `POST /api/workspace/commit` → Commit changes (Git integration planned)

3. **Governance & Curation API**

   * `GET /api/governance/ballots` → Active proposals
   * `POST /api/governance/ballots/:id/vouch` → Vouch with trust validation
   * `GET /api/contributions/approved` → Approved contributions

4. **PinkSync Service**

   * Socket.io or equivalent for multi-user collaboration
   * Frontend hooks already prepared to connect

5. **Gemini API Proxy**

   * Secure backend proxy for Gemini API
   * Prevents exposing API key on client side

---

## 📌 Deployment Notes

* **Frontend**: Deployable on Vercel or Cloud Run (current: Vercel staging, may migrate fully to GCP).
* **Backend**: FastAPI services structured for Cloud Run + Cloud SQL.
* **Real-time (PinkSync)**: Node.js service deployable on Cloud Run with WebSocket support.
* **Environment variables**: Required for Gemini API, Auth secrets, DB URLs.

---

## 🧑‍🤝‍🧑 Team Instructions

* **Frontend Developers**: Replace mocked services with real API calls once endpoints are live.
* **Backend Engineers**: Implement service logic inside FastAPI scaffolds, connect to DB, and expose APIs.
* **DevOps**: Configure secrets in Google Cloud, ensure CI/CD pipeline for both frontend & backend.
* **Contributors**: Use `pinkflow` workspace as your entry point – governance, contributions, and code review run through MBTQ.dev.

---

## 🌍 Vision

MBTQ.dev is not just another SaaS – it’s a **Deaf-First innovation hub**. With **unified identity (DeafAuth)**, **trusted governance (FibonRose)**, **real-time sync (PinkSync)**, and **business AI agents (360Magicians)**, this ecosystem creates the infrastructure for accessible, compliant, and scalable Deaf-led entrepreneurship globally.
