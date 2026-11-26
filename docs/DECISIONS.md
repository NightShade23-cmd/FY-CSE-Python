# ARCHITECTURAL DECISIONS & STATUS REGISTER
### Document: `docs/DECISIONS.md`

This document maintains the living record of architectural decisions, technical trade-offs, scope boundaries, and open questions for the **Gym Management System**.

---

## Decision Status Legend

Every item in this register is categorized into one of three statuses:
* **`[CONFIRMED]`** — Approved, binding decision that directly guides current implementation.
* **`[OPTIONAL / FUTURE]`** — Valid concept or feature explicitly deferred beyond Version 1.
* **`[OPEN / TBD]`** — Decision deliberately left open until a specific implementation milestone is reached.

---

## 1. Hosting, Deployment & Infrastructure Decisions

### Decision 1.1: Single-Gym Architecture `[CONFIRMED]`
* **Decision:** The application will manage operations for **exactly one gym**.
* **Rationale:** Modeling multi-branch gyms introduces unnecessary schema complexity (branch IDs, inter-branch transfers, role hierarchies) that distracts from the core academic and operational goals.
* **Impact:** No branch identifiers or multi-tenant database logic will be written.

### Decision 1.2: Local Wi-Fi Network Hosting on Owner's Laptop `[CONFIRMED]`
* **Decision:** In Version 1, the primary server will be the gym owner's laptop/PC running the Flask application locally.
* **Network Setup:** The laptop connects to the gym's existing Wi-Fi router. Members on the gym Wi-Fi access the registration page from their phones using the laptop's local IP address (e.g., `http://192.168.1.50:5000`). The administrator accesses the system via `localhost` or from another authorized device on the same network.
* **Availability Note:** The server computer must remain powered on and running the Flask process for the site to be reachable. Application data is persisted locally on the server computer, while backup and recovery arrangements remain `[OPEN / TBD]`.

### Decision 1.3: Public Cloud Hosting Deferred for Version 1 `[CONFIRMED]`
* **Decision:** Deployment to public cloud providers (Vercel, Render, AWS, Heroku, etc.) is **deferred for Version 1**.
* **Clarification:** Public cloud hosting is **not permanently rejected**. The codebase will maintain a clean, portable architecture (environment-based configuration, separate data and media directories) so that the application can transition to cloud hosting in a future version without rewriting business logic.

### Decision 1.4: Android Phone as Temporary Alternative Server `[OPTIONAL / FUTURE]`
* **Decision:** Running the Flask server on an Android phone is an optional, experimental idea for later exploration.
* **Constraint:** It is **not** the primary deployment plan. Technical issues such as Android background process management, battery optimization, thermal throttling, and local network exposure must be evaluated in a separate experiment.

### Decision 1.5: Wi-Fi Guest Network Client Isolation Awareness `[CONFIRMED]`
* **Decision:** During network testing, the team will check whether the gym router's guest Wi-Fi enforces "Client Isolation".
* **Impact:** Client isolation blocks wireless clients from communicating with local network servers. If enabled, phones cannot open the laptop's server IP. The gym must either configure router permissions or connect phones and the server to an appropriate non-isolated network segment.

### Decision 1.6: Zero-Cost Policy (No Paid APIs or Services) `[CONFIRMED]`
* **Decision:** The project will strictly prioritize free, local, open-source tools and existing gym equipment.
* **Rule:** No paid hosting subscriptions, new router purchases, or paid third-party APIs (such as cloud image generation) may be introduced without prior explicit approval.

---

## 2. UI/UX Ownership & Design Workflow Decisions

### Decision 2.1: Exclusive Visual Ownership by Project Owner `[CONFIRMED]`
* **Decision:** The project owner retains **100% personal control** over visual design, color palettes, typography, branding, layouts, visual assets, and overall aesthetic identity.
* **Rule for AI Agents:** AI agents must **never** generate generic AI-styled websites, colorful gradients, decorative card themes, or pre-built dashboard templates.

### Decision 2.2: Plain, Functional Structure in Phase 1 `[CONFIRMED]`
* **Decision:** Initial development will focus strictly on semantic HTML structure, functional routing, form validation, and data display tables.
* **Styling Boundary:** Only minimal, practical CSS is permitted where required for basic readability, spacing, and mobile responsiveness. Final visual design is deferred until the structural skeleton is complete.

### Decision 2.3: Minimal Landing Page vs. Separate Admin Dashboard `[CONFIRMED]`
* **Decision:** The public root URL (`/`) will serve a **minimal landing page** displaying the gym's name and links to Member Registration and Admin Login.
* **Boundary:** The Admin Dashboard will be an authenticated, separate route (`/admin/dashboard`) and must **never** be made the default homepage.

### Decision 2.4: Optional Design Tools & Translation Workflow `[OPEN / TBD]`
* **Context:** The owner will develop visual references independently.
* **Exploration Tools:** **Canva**, **Figma**, and **Google Stitch** are optional tools for the owner's design exploration, not mandatory project dependencies.
* **Translation Workflow:** The owner may use **ChatGPT** to review visual mockups and translate them into technical implementation prompts; Antigravity will then implement the approved HTML/CSS/Jinja changes.

---

## 3. Member & Trainer Workflow Decisions

### Decision 3.1: Public Registration Flow with "Pending Approval" Status `[CONFIRMED]`
* **Decision:** Prospective members submit registrations on their phones. Submissions enter the database with the status **`Pending Approval`**.
* **Security Rule:** The public registration page provides submission feedback only; it never exposes existing member records, other pending applications, or administrative controls.

### Decision 3.2: Mandatory Profile Photo, Gender, and Blood Group `[CONFIRMED]`
* **Profile Photo:** Mandatory at registration, with explicit user consent displayed on the form.
* **Gender:** Mandatory field with exactly three options: `Male`, `Female`, and `Non-binary`.
* **Blood Group:** Mandatory field with exactly eight standard medical options: `A+`, `A-`, `B+`, `B-`, `AB+`, `AB-`, `O+`, and `O-`. No "Unknown" option.
* **Blood Group Medical Restriction:** Blood group is strictly a medical/emergency record; it must **never** be used in fitness algorithms, BMI remarks, or trainer matching.

### Decision 3.3: Baseline Measurements vs. Monthly Fitness History `[CONFIRMED]`
* **Decision:** Registration height and weight are permanently recorded as **baseline measurements**.
* **History:** Monthly assessment updates are stored as new records in a dedicated `fitness_assessments` table to allow tracking changes over time.
* **BMI:** Informational calculation ($BMI = \frac{\text{weight in kg}}{(\text{height in m})^2}$) with age-appropriate remarks. BMI must **never** be used for trainer assignment or medical diagnosis.

### Decision 3.4: Soft Deactivations (No Normal Hard Deletes) `[CONFIRMED]`
* **Decision:** Members leaving the gym are deactivated (`status = 'Inactive'`).
* **Preservation:** Deactivated members are excluded from active workload tallies and active member counts, but all historical records (memberships, payments, attendance, fitness assessments) remain permanently in the database.

### Decision 3.5: Transparent Rule-Based Trainer Assignment `[CONFIRMED]`
* **Decision:** Trainer suggestions will be computed using **simple, transparent Python rules** (`if`/`else` statements, loops, dictionaries, and sorting).
* **Machine Learning Excluded:** No neural networks, ML models, or opaque weighted scoring algorithms.
* **Matching Factors:** Member fitness goal matched to trainer specialty, member fitness level (used only when matching against an explicitly defined trainer specialization, if such a category is approved later), shift preference (`Morning` / `Evening`), trainer availability, and remaining capacity.
* **Workload Balancing:** Eligible trainers are ranked to favor those with lower relative workloads.
* **Display-Only Fields (Strictly Non-Scoring):** The trainer's experience level, years of experience, qualifications, and certifications are profile display fields only; they must **never** influence trainer assignment, scoring, or workload ranking.
* **Assignment Limits:** Maximum **one trainer** per member. A trainer is **optional** (members can opt out).
* **Admin Override:** The system provides a suggestion; the administrator makes the final confirmation or manual adjustment.

### Decision 3.6: Standardized Illustrated Portraits & Early Proof of Concept `[CONFIRMED]`
* **Desired Functional Result:** Provide standardized, clean, polished digital illustrated portraits of members placed against a plain solid background for visual consistency across profile pictures instead of displaying unrelated raw photographs. Comic, sketch, and 3D styles are explicitly excluded.
* **Experimental Processing Techniques & Proposed Tools:** The proposed pipeline relies on local open-source Python libraries (**MediaPipe** for person segmentation, **OpenCV** for artistic digital filtering, and **Pillow** for cropping, resizing, and compositing over a solid plain-color background).
* **Proof of Concept Requirement:** While the desired functional result is a key proposed application feature, the specific processing techniques and proposed Python libraries are experimental. Because third-party libraries (especially MediaPipe and OpenCV wheels) can have compatibility hurdles across newer Python releases (such as Python 3.15 on Windows), an **early proof-of-concept (POC)** will test library installation, execution stability, and visual output quality before integrating them into the core registration flow.

---

## 4. Membership, Payment, Attendance & Equipment Decisions

### Decision 4.1: Four Standard Membership Plans `[CONFIRMED]`
* **Decision:** Plans will be **Monthly** (1 month), **Quarterly** (3 months), **Half-yearly** (6 months), and **Annual** (12 months). Expiry dates are calculated automatically.

### Decision 4.2: Manual Payment Recording (Cash and UPI) `[CONFIRMED]`
* **Decision:** No online payment gateway (Stripe, Razorpay, etc.) in Version 1.
* **Process:** Supported methods are **Cash** and **UPI**. The application can display the gym's UPI QR code. The administrator manually verifies payment and records the transaction (`Paid`, `Pending`, or `Partially Paid`).

### Decision 4.3: Attendance Integrity Safeguards `[CONFIRMED]`
* **Decision:** Attendance logic will prevent duplicate active check-ins and invalid check-outs, flag visits left open past gym hours, and provide daily rosters and monthly calendar views.

### Decision 4.4: Dual Equipment Inventory Strategy `[CONFIRMED]`
* **Quantity Tracking:** Weights and accessories (dumbbells, weight plates, kettlebells) are managed by specification and quantity.
* **Individual Unit Tracking:** Complex machines (treadmills, cable machines) are tracked as distinct units with individual maintenance histories.

### Decision 4.5: Practical Academic Analytics `[CONFIRMED]`
* **Decision:** **Pandas**, **NumPy**, **Matplotlib**, and **Seaborn** must be used meaningfully on real database records for aggregations, statistical summaries, downloadable CSV/Excel reports, and visualization charts (membership growth, attendance trends/heatmaps, workload charts).

---

## 5. Technology & Development Workflow Decisions

### Decision 5.1: Core Stack `[CONFIRMED]`
* **Language:** Python 3.15.2
* **Backend:** Flask 3.1.3
* **Templates:** Jinja2
* **Frontend:** Semantic HTML5, CSS3, vanilla JavaScript (no React/Vue/Angular).
* **Database:** SQLite.

### Decision 5.2: Database Access Method (Direct SQL vs. SQLAlchemy) `[OPEN / TBD]`
* **Context:** The owner is learning SQL and database design.
* **Status:** Kept open until the database design milestone. If `Flask-SQLAlchemy` is selected, it must be accompanied by explicit explanations of the underlying SQL queries so that database learning is preserved.

### Decision 5.3: AI Toolchain & Model Guidelines `[CONFIRMED]`
* **Primary Coding Tool:** VS Code with Google Antigravity extension.
* **Agent Management:** Antigravity App (when useful for higher-level orchestration).
* **Model Preference:** **Gemini 3.8 Flash** (aligned with the user's available plan). Code will remain clean and standard, never tied to model-specific features.

### Decision 5.4: Beginner-Friendly Development & Approval Cycle `[CONFIRMED]`
* **Cycle:** Inspect $\rightarrow$ Plan $\rightarrow$ Await User Approval $\rightarrow$ Implement $\rightarrow$ Test $\rightarrow$ Explain in plain English $\rightarrow$ Propose Git commit.

---

## 6. Traceability Table ("Earlier Proposal vs. Later Decision")

| Topic | Original Proposal | Confirmed Later Decision | Classification |
|---|---|---|---|
| **Gym Branches** | Multi-branch listed in Scope Boundaries. | Strictly models **one single gym**. | `[CONFIRMED]` |
| **Landing Page vs. Dashboard** | Minimal main page instead of heavy dashboard. | Public landing page and Admin Dashboard are **strictly separate routes**. | `[CONFIRMED]` |
| **User Accounts** | Members have no login; Admin has login. | **Admin only** logs in. No member or trainer accounts. | `[CONFIRMED]` |
| **Registration Flow** | Member registers; admin manages/approves. | Submissions start as **`Pending Approval`** in an admin queue. | `[CONFIRMED]` |
| **Trainer Experience** | Listed as trainer profile info. | Display-only; **strictly non-scoring** in assignment logic. | `[CONFIRMED]` |
| **Trainer Assignment Option** | Automated suggestion. | Trainer is **optional**; max 1 trainer per member; workload balanced. | `[CONFIRMED]` |
| **Hosting Model** | Unspecified. | **Local Wi-Fi hosting** on laptop; cloud deferred for V1 (portable). | `[CONFIRMED]` |
| **UI Design Ownership** | Focus on functionality over visual design. | Owner has **100% visual ownership**; plain HTML structure first. | `[CONFIRMED]` |
| **Illustrated Portraits** | MediaPipe + OpenCV + Pillow pipeline. | Retained as key feature, marked for **early Proof of Concept (POC)**. | `[CONFIRMED]` |
| **Database Access Library** | SQLite specified. | Raw `sqlite3` vs. `Flask-SQLAlchemy` kept **OPEN / TBD** for learning. | `[OPEN / TBD]` |

---

## 7. Open Decisions Register (`[OPEN / TBD]`)

The following decisions are intentionally left open and will be resolved during their respective development milestones:

1. **Predefined Fitness Goals List:**
   * *Status:* `[OPEN / TBD]`
   * *Target Milestone:* Member registration form design.
   * *Options Discussed:* Weight gain, weight loss, being fit/general fitness, and professional training. The final list of options remains to be determined.
2. **Trainer Specialization Taxonomy & Goal Mapping:**
   * *Status:* `[OPEN / TBD]`
   * *Target Milestone:* Trainer management module design.
   * *Options Discussed:* Newcomers, younger members, professionals, and ladies. The final taxonomy of specialties and matching rules to fitness goals remains to be determined. (Note: Specific coaching labels like Strength & Conditioning or Rehabilitation are not decisions made by the project owner).
3. **Application Decline / Deferral Workflow:**
   * *Status:* `[OPEN / TBD]`
   * *Target Milestone:* Admin registration review implementation.
   * *Context:* What specific status, notification, or archive step occurs when a registration is not approved.
4. **Database Access Layer (`sqlite3` vs. `Flask-SQLAlchemy`):**
   * *Status:* `[OPEN / TBD]`
   * *Target Milestone:* Database schema creation milestone.
   * *Evaluation Criteria:* Maximizing SQL learning and conceptual understanding vs. query convenience.
5. **Local Network Addressing (`gym.local` vs. Local IP):**
   * *Status:* `[OPEN / TBD]`
   * *Target Milestone:* Local network deployment testing.
   * *Context:* Whether to use mDNS/local hostname resolution or a fixed local IP address.
6. **Local Backup & Recovery Strategy:**
   * *Status:* `[OPEN / TBD]`
   * *Target Milestone:* Deployment & security preparation.
   * *Context:* Automated or manual local file backups for `gym.db` and uploaded media files.
7. **Equipment Illustration Graphic Sources:**
   * *Status:* `[OPEN / TBD]`
   * *Target Milestone:* Equipment management module.
   * *Context:* Sourcing consistent visual icons or illustrations for weights and machines.
8. **UI Design Translation Workflow:**
   * *Status:* `[OPEN / TBD]`
   * *Target Milestone:* UI/UX styling phase (after functional skeleton is built).
   * *Context:* Formalizing the process of taking Canva/Figma mockups through ChatGPT for implementation by Antigravity.
9. **Membership Activation vs. Pending/Partial Payment:**
   * *Status:* `[OPEN / TBD]`
   * *Target Milestone:* Member approval workflow design.
   * *Context:* Defining the exact operational relationship between payment confirmation and member activation. The system must not assume that full payment is mandatory before activation; rules for activating members with `Pending` or `Partially Paid` status remain to be determined.
10. **Initial Administrator Account Creation & Credential Management:**
    * *Status:* `[OPEN / TBD]`
    * *Target Milestone:* Authentication & admin setup milestone.
    * *Context:* How the initial administrator username and password will be seeded or created (e.g., setup CLI script, initial environment configuration, or first-run setup wizard), and how secure credential updates will be managed.
11. **Required Equipment Maintenance Information:**
    * *Status:* `[OPEN / TBD]`
    * *Target Milestone:* Equipment management module.
    * *Context:* Establishing the exact mandatory schema for maintenance logs (e.g., date, description of work, equipment status) versus optional/open fields such as maintenance cost and technician details.
12. **Compatibility Testing of Installed Python Version with Analytics & Image Libraries:**
    * *Status:* `[OPEN / TBD]`
    * *Target Milestone:* Analytics & image-processing setup milestone.
    * *Context:* Verifying the compatibility of Python 3.15.2 with required data libraries (Pandas, NumPy, Matplotlib, Seaborn) and image-processing packages (MediaPipe, OpenCV, Pillow) on 64-bit Windows, identifying any pre-compiled wheel requirements or fallback strategies early.
