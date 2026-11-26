# AGENTS.md — AI Agent Operating Instructions
### Gym Management System

Welcome to the **Gym Management System** project repository. This document is the permanent operating manual and set of rules of engagement for all AI coding assistants (including Antigravity and any future agents) working in this workspace.

---

## 1. Project Overview & Core Philosophy

1. **What We Are Building:**
   A modular, Python-based web application to organize the day-to-day operations of a gym. It combines core administrative workflows (members, trainers, memberships, payments, attendance, equipment inventory) with real data analytics and reporting using **Pandas**, **NumPy**, **Matplotlib**, and **Seaborn**.
2. **Architecture & Scope:**
   - **Single Gym Only:** Strictly models one gym. It does not support multiple gym branches.
   - **Local Wi-Fi Network Hosting:** In Version 1, the application is self-hosted on the gym owner's laptop/PC and accessed over the gym's local Wi-Fi router.
   - **Two Access Areas:** A public member self-registration page (accessed via phones on gym Wi-Fi) and a password-protected Administrator Panel.
   - **No Member or Trainer Logins:** In Version 1, members and trainers do not have individual user accounts. Only the administrator logs in.
3. **The User & Educational Mandate:**
   - The project owner is a **beginner developer** learning Python, web development, SQL, and database concepts.
   - You must write clean, simple, understandable Python and frontend code.
   - Avoid clever, complex abstractions or magic frameworks that are difficult to explain in an academic setting.
   - Explain your code, file purposes, and architectural choices clearly in plain English, avoiding unnecessary technical jargon.

---

## 2. Absolute Ground Rules (The "Never" List)

Any agent working in this repository must strictly obey these boundaries:

1. **Never Make Unapproved Changes:**
   Always inspect first, present a clear step-by-step plan, and wait for explicit user approval before creating or modifying files.
2. **Never Invent Visual Design or Styling:**
   - The project owner retains **100% personal ownership** of visual design, color palettes, typography, branding, layouts, and visual assets.
   - Do **NOT** invent a generic "AI-generated" website design, modern gradient aesthetic, or pre-built dashboard template.
   - For initial development, build **strictly plain, functional HTML structures** (clean forms, tables, basic buttons, and simple navigation). Visual styling is deferred until the owner provides approved design references.
3. **Never Run Git Write Operations Automatically:**
   - Read-only Git inspection commands (`git status`, `git log`, `git diff`, `git branch` without modification arguments) are permitted to inspect repository state.
   - Explicit approval is strictly required before running any Git write operations or branch-changing operations (such as `git add`, `git commit`, `git push`, `git checkout`, `git switch`, `git merge`, or creating/deleting branches).
   - After completing an approved task, report your changes, explain what was done, and propose a clean commit message, then wait for explicit user instruction before any Git action.
4. **Never Introduce Paid Tools, APIs, or Services:**
   - Strict zero-cost policy.
   - Do not add paid cloud services, paid image-generation APIs, or paid third-party dependencies without explicit approval.
5. **Never Assume Cloud Hosting for Version 1:**
   - Do not deploy to Vercel, Render, AWS, or other cloud platforms.
   - The primary server is the owner's laptop on the local Wi-Fi network.
   - Keep the codebase device-independent so that future cloud hosting remains possible without rewriting business logic, but do not make cloud services a requirement now.
6. **Never Hard-Delete Member Records:**
   - Always use **soft deactivations** (setting a member's status to `inactive`).
   - Historical records (previous memberships, payments, attendance, and fitness assessments) must be permanently preserved.
7. **Never Make the Dashboard the Homepage:**
   - The public landing page is a minimal page displaying gym identity and navigation links (to Member Registration and Admin Login).
   - The administrative dashboard is a separate, protected page accessible only after login.
8. **Never Introduce Machine Learning for Trainer Matching:**
   - Trainer recommendations must use transparent, deterministic Python rules (`if`/`else` logic, loops, dictionaries, and sorting).
   - Trainer experience and qualifications are profile display fields only, **never** numerical scoring factors.

---

## 3. Mandatory Context Reading

Before undertaking any substantial planning or coding task, **every AI agent must read:**
1. `AGENTS.md` (this file)
2. `docs/PROJECT_BRIEF.md` (the complete functional and technical specification)
3. `docs/DECISIONS.md` (the register of confirmed decisions, changed requirements, and open questions)

Do not assume you know the requirements from prior conversational memory. Always check these repository files.

---

## 4. Standard Agent Task Cycle

All development tasks must strictly follow this disciplined, step-by-step cycle:

```
[1. Inspect Workspace] ──> [2. Present Plan] ──> [3. Await User Approval]
                                                          │
[6. Propose Git Commit] <── [5. Explain & Test] <── [4. Implement in Steps]
```

1. **Inspect:** Examine the workspace, existing files, virtual environment, and Git status before planning.
2. **Plan:** Present a detailed, beginner-friendly plan specifying exactly which files will be created or modified, what logic will be written, and what concepts will be used.
3. **Wait for Approval:** Stop and ask the user for approval. Do not write code until approval is given.
4. **Implement:** Write clean, modular, well-commented code in small, verifiable steps.
5. **Explain & Test:** Run tests, verify functionality, and explain what the code does in simple terms.
6. **Propose Git Commit:** Summarize the changes and propose a clean Git commit message. Wait for the user to instruct you to commit.

---

## 5. UI/UX Workflow & Design Ownership

- **Owner Control:** The user decides the visual direction using optional tools such as **Canva**, **Figma**, or **Google Stitch**.
- **Translation Pipeline:** The user may use **ChatGPT** to review designs and help translate visual concepts into implementation instructions.
- **Agent's Role:** Antigravity implements approved HTML, CSS, JavaScript, and Jinja templates based strictly on the user's approved instructions.
- **Initial Phase:** Focus purely on semantic HTML, form structure, input validation, table displays, and functional routing. Minimal layout styling is permitted only for usability and readability.

---

## 6. Coding & Architectural Standards

1. **Modularity:**
   Do not dump all routes, database calls, and business logic into a single monolithic file. Organize the application cleanly:
   - `app/` — Application package
   - `app/routes/` — Route handlers (split logically: public, admin, members, trainers, etc.)
   - `app/models/` or `app/database/` — Database schemas and queries
   - `app/services/` — Business logic (e.g., trainer assignment algorithm, analytics helpers)
   - `app/templates/` — Jinja2 HTML templates
   - `app/static/` — Static assets (CSS, JS, images)
2. **Database Integrity:**
   - Primary database is **SQLite**.
   - Foreign keys must be enforced.
   - Maintain historical logs: membership renewals, payment transactions, visit check-ins, and monthly fitness measurements.
   - The choice between raw `sqlite3` and `Flask-SQLAlchemy` will be decided during the database design milestone to ensure SQL fundamentals are properly learned.
3. **Security & Validation:**
   - Server-side validation is mandatory for all form submissions.
   - Admin routes must be strictly protected on the server side (not just hidden in the frontend UI).
   - Sanitize all uploaded files (profile photos). Store uploaded media safely outside public source directories.
   - Never hardcode secret keys or sensitive configuration in code.
4. **Academic Analytics (Pandas / NumPy / Matplotlib / Seaborn):**
   - Must be used meaningfully on real database records, not as decorative or artificial imports.
   - Pandas: DataFrames, filtering, groupings, summary statistics, CSV and Excel report exports.
   - NumPy: Mean, median, standard deviation calculations for attendance and fitness data.
   - Matplotlib & Seaborn: Visualizations (membership growth, attendance trends, trainer workload distribution, payment collections).

---

## 7. Development Environment & Tooling

- **Operating System:** Windows 10, 64-bit
- **Project Directory:** `D:\GymManagementSystem`
- **Python Version:** Python 3.15.2
- **Framework:** Flask 3.1.3
- **Primary Editor:** VS Code with the official **Google Antigravity** extension
- **Agent Management:** **Antigravity App** (for broader agent or project tasks when helpful)
- **Model Preference:** **Gemini 3.8 Flash** (aligned with the user's current plan; code must remain standard and reproducible, never tied to model-specific quirks)
- **Git:** Git for Windows (branch `main`, tracking private GitHub remote `origin/main`). Read-only inspection commands are allowed; write and branch-changing operations require explicit user approval.
