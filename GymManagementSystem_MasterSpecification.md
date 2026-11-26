# GYM MANAGEMENT SYSTEM
### Project Proposal — Version 1 (Initial Scope)

## 1. Project Overview

The proposed project is a Python-based web application designed to simplify and organize the day-to-day operations of a gym.

The system will allow gym administrators to manage member registrations, trainer assignments, memberships, payments, attendance and equipment inventory through a centralized platform.

It will also include data analysis and visualization features using Python libraries such as Pandas, NumPy, Matplotlib and Seaborn.

The application will primarily be designed for gym owners and administrators. Members will be able to submit their registration details through a public registration page, while administrators will manage and approve their applications.

**Main objective:** To develop a structured, user-friendly gym management application that combines everyday gym administration with useful Python-based data processing and analytics.

---

## 2. Technology Stack

The project will use the following technologies:

| Technology | Purpose |
|---|---|
| Python | Main programming language and application logic |
| Flask | Python web framework for connecting the website with the backend |
| SQLite | Database for storing gym records |
| HTML | Structure of webpages |
| CSS | Styling and page layouts |
| JavaScript | Frontend interactivity and automatic field calculations |
| Jinja | Displaying Python data inside HTML templates |
| Pandas | Data manipulation, analysis and report generation |
| NumPy | Numerical and statistical calculations |
| Matplotlib | Data visualization and charts |
| Seaborn | Statistical graphs and visualizations |
| Pillow, OpenCV and MediaPipe | Member portrait processing and image handling |

C++ will not be required.

The project will prioritize simple, modular and understandable Python code.

---

## 3. Application Structure and Access

The application will have two main entry points:

**A. Public Member Registration**
- New members can open the registration page.
- They can enter their personal, contact and fitness information.
- They must upload a photograph.
- Applications will be submitted for administrator approval.
- Members will not require individual login accounts in Version 1.

**B. Administrator Panel**
- Secure administrator login.
- Access to all management modules.
- Review and approve member applications.
- Manage members, trainers, memberships, payments, attendance and equipment.
- Generate reports and view analytics.

The main application page will be minimal, displaying the gym name and navigation to different management sections. A statistics-heavy dashboard will not be the homepage in Version 1.

---

## 4. Main Application Modules

### Module 1: Member Management

This module will maintain the records and profiles of all gym members.

**Member information:**

| Category | Information |
|---|---|
| Personal details | Member ID, full name, date of birth, automatically calculated age, gender and profile photograph |
| Gender | Male, Female and Non-binary |
| Contact details | Phone number, email and address |
| Emergency information | Emergency contact name, relationship and phone number |
| Health information | Blood group, height, weight and calculated BMI |
| Fitness information | Fitness goal and current fitness level |
| Membership information | Selected membership plan, joining date and expiry date |
| Trainer information | Trainer requirement, assigned trainer and preferred training shift |
| Status | Pending approval, active or inactive |

Blood group options will include A+, A-, B+, B-, AB+, AB-, O+ and O-.

**Automatic calculations and fitness tracking:**
- Age will be calculated automatically from the date of birth.
- BMI will be calculated from height and weight.
- An explanatory BMI remark may be displayed using an appropriate age-based reference.
- The initial height and weight will be retained as baseline measurements.
- Monthly fitness assessments will record updated height and weight.
- Historical measurements will be available to track changes over time.

BMI will be informational and will not determine trainer assignment.

**Member management functionalities:**

1. Add new members.
2. Update existing member details.
3. Deactivate or reactivate members.
4. Search members by name or ID.
5. Filter members by membership type and status.
6. View individual member profiles.
7. Identify memberships expiring within the next 7 or 30 days.
8. Maintain fitness assessment history.

Deactivation will normally be used instead of permanently deleting member records, so historical information remains available.

### Special Feature: Standardized Illustrated Member Portraits

One distinctive feature of the application will be automatic conversion of member photographs into standardized illustrated portraits.

The objective is to give every member a consistent profile-picture style instead of displaying unrelated photographs.

Proposed process:
1. Member uploads a photograph during registration.
2. The system separates the person from the original background.
3. Image processing applies a consistent illustrated appearance.
4. The person is placed against a selected plain-colour background.
5. The generated portrait is saved and displayed in the member profile.

The intended style is a clean, polished illustrated digital portrait. Comic, sketch, and 3D-inspired styles are excluded.

Proposed Python tools:
- MediaPipe for person segmentation.
- OpenCV for artistic image processing.
- Pillow for cropping, resizing and background composition.

The feature will use free local-processing tools rather than a paid image-generation API. Its visual quality and reliability will be tested in an early prototype.

---

### Module 2: Trainer Management

This module will store trainer information and manage member assignments.

**Trainer information:**
- Trainer ID and name.
- Contact information.
- Qualifications and certifications.
- Years of experience.
- Training specializations.
- Available training shifts.
- Maximum member capacity.
- Current assigned-member count.
- Availability status.

Trainer experience and qualifications will be displayed as profile information, not used as numerical scoring factors in the assignment algorithm.

**Trainer assignment system:**

The application will suggest trainers automatically based on member requirements.

Member registration will collect:
- Fitness goal.
- Current fitness level: Beginner, Intermediate or Advanced.
- Whether a trainer is required.
- Preferred training shift.

The trainer recommendation system will consider:
1. Trainer specialization and member fitness goal.
2. Relevant beginner/intermediate/advanced coaching specialization, where recorded.
3. Preferred training shift.
4. Trainer availability.
5. Remaining member capacity.
6. Current trainer workload.

Eligible trainers will be ranked, giving preference to suitable trainers with lower relative workloads.

The recommendation will be implemented using basic Python logic such as conditions, loops, lists, dictionaries and sorting. Administrators will be able to confirm or manually change the suggested assignment.

**Training schedule:**

- Morning and Evening shifts.
- Gym operates six days a week: Monday to Saturday.
- Sunday will be a weekly holiday.
- No individual preferred training days will be considered in Version 1.

---

### Module 3: Membership and Payment Management

Membership and payment functions will be available under one application module, while their records will be maintained separately.

**Membership plans:**

| Plan | Duration |
|---|---|
| Monthly | 1 month |
| Quarterly | 3 months |
| Half-yearly | 6 months |
| Annual | 12 months |

**Membership functionalities:**
- Register a new membership.
- Renew existing memberships.
- Calculate membership expiry dates.
- Maintain previous membership records.
- Track active and expired memberships.
- Display upcoming expiry notifications.

**Payment management:**

Online payment-gateway integration will not be included.

Supported payment methods:
- Cash.
- UPI.

The application can display the gym's UPI QR code. Administrators will manually confirm and record successful payments.

Payment information will include:
- Member ID.
- Amount.
- Payment date.
- Payment method.
- Payment status (Paid, Pending or Partially Paid).

Previous payment records will remain available for reference.

---

### Module 4: Attendance Management

This module will record member visits and maintain attendance history.

Each attendance record will contain:
- Attendance ID.
- Member ID.
- Member name.
- Date.
- Check-in time.
- Check-out time.
- Duration of visit.

**Functionalities:**
- Record member check-in.
- Record member check-out.
- View daily attendance.
- Search attendance history.
- View individual member attendance.
- Display attendance through a monthly calendar.
- Identify missing check-outs.

The system will prevent duplicate active check-ins and invalid check-outs.

Attendance information will also be used for statistical analysis and reports.

---

### Module 5: Equipment Management

This module will maintain gym equipment inventory and maintenance records.

Equipment will be organized into categories.

**Weights and accessories:**
- Dumbbells of different weights.
- Weight plates.
- Barbells.
- Straight bars.
- EZ curl / zigzag bars.
- Kettlebells.

**Machines:**
- Treadmills.
- Exercise bikes.
- Leg press machines.
- Chest press machines.
- Cable machines.

**Cable attachments and extensions:**
- Straight bars.
- Rope attachments.
- V-shaped handles.
- Other cable-machine attachments.

**Equipment information:**
- Equipment ID.
- Equipment name.
- Category.
- Illustration.
- Quantity or individual unit identification.
- Weight or specification, where applicable.
- Working status.
- Purchase date, where available.
- Last maintenance date.
- Maintenance history.

Equipment status:
- Working.
- Under maintenance.
- Out of service.

The module will support:
- Adding and updating equipment.
- Managing quantities.
- Viewing equipment by category.
- Updating equipment status.
- Recording maintenance activities.
- Identifying unavailable equipment.

Consistent illustrations will be displayed alongside equipment names for easier identification.

Quantity-based equipment, such as dumbbells, will be managed by weight and quantity. Individual machines will be tracked separately to maintain their maintenance history.

---

### Module 6: Reports and Data Analytics

This module will demonstrate the practical use of Python's data-processing and visualization libraries.

**Pandas — Main data analysis library**

Pandas will retrieve records from SQLite into DataFrames and perform operations such as:
- Filtering and sorting member records.
- Counting active and expired memberships.
- Analysing membership-plan distribution.
- Calculating trainer workloads.
- Analysing attendance records.
- Summarizing payment collections.
- Identifying equipment maintenance status.
- Generating downloadable CSV and Excel reports.

**NumPy — Numerical operations**

NumPy will be used for:
- Mean and median calculations.
- Minimum and maximum values.
- Standard deviation.
- Numerical summaries of attendance and other gym statistics.

**Matplotlib and Seaborn — Visualizations**

Possible visualizations include:
- Membership distribution charts.
- Monthly membership growth.
- Attendance trends.
- Daily and monthly attendance comparisons.
- Trainer workload comparisons.
- Payment and revenue summaries.
- Equipment-status charts.
- Attendance heatmaps.

The aim is to demonstrate meaningful use of these libraries on actual application records rather than using them artificially.

---

## 5. Proposed Database

SQLite will be used as the primary database.

The main database tables are expected to include:

1. Members
2. Trainers
3. Membership Plans
4. Membership Records
5. Payments
6. Attendance
7. Equipment
8. Equipment Maintenance
9. Fitness Assessments
10. Trainer Assignments
11. Trainer Availability

The exact columns, relationships and database structure will be finalized during the design stage.

Historical information such as previous memberships, payments, attendance and fitness assessments will be preserved.

Deactivated members will be excluded from current active-member statistics and workloads, while their historical records remain accessible.

---

## 6. Python Concepts Demonstrated

The project will make practical use of several Python programming concepts:

| Concept | Application |
|---|---|
| Variables and data types | Storing member and gym information |
| Lists and dictionaries | Organizing and processing records |
| Functions | Reusable application operations |
| Conditional statements | Validation and trainer assignment |
| Loops | Processing member and equipment records |
| Searching and sorting | Member and trainer management |
| Date and time operations | Age, membership expiry and attendance |
| Exception handling | Managing errors and invalid input |
| Modules | Organizing the application |
| SQLite and SQL | Database operations |
| Pandas | Data manipulation and reporting |
| NumPy | Numerical calculations |
| Matplotlib and Seaborn | Data visualization |

The codebase will be divided into manageable modules rather than placing all functionality into a single large Python file.

---

## 7. Scope Boundaries

To keep Version 1 achievable and understandable, the following features will not be included initially:

- Diet-plan management.
- Online payment processing.
- Separate member login accounts.
- Separate trainer login accounts.
- Automatic temporary substitute-trainer management.
- Multiple gym branches.
- Complex AI or machine-learning-based trainer recommendations.

Some of these may be considered for a future version if time and project requirements allow.

---

## 8. Development Philosophy

The project will be developed using AI-assisted tools for the initial prototype, but the final code and architecture should remain understandable and reproducible through manual programming.

The main priorities are:

- Simple Python logic.
- Modular and structured code.
- Meaningful use of Pandas, NumPy, Matplotlib and Seaborn.
- Proper database relationships.
- Reliable data handling and validation.
- A functional and user-friendly web application.
- Clear understanding of every major function and operation.

The final objective is not merely to produce a visually attractive website, but to develop a functional gym-management application whose implementation can be understood and explained by the project team.

---

**Project Status:** Initial Version 1 scope proposed. Detailed registration workflow, database schema and trainer-assignment logic will be finalized before implementation.

---

# PROJECT ADDENDUM — LATER CONFIRMED DECISIONS AND IMPLEMENTATION GUIDANCE

**Authority and preservation rule**

The complete Version 1 proposal above is retained as supplied. Its original wording and organization have not been rewritten. This addendum records later discussions and clarifications. Where a later confirmed decision below updates or conflicts with an earlier statement in the original proposal, follow the later decision. Do not silently remove original requirements; record any future scope change in `docs/DECISIONS.md`.

## A. Overall scope and development approach

1. The application is for **one gym only**. The gym may have multiple real-world branches, but this project must not manage or model multiple branches.
2. Build a complete, modular prototype first. Optional functionality can later be removed or simplified for the college submission. Keep modules sufficiently independent that this is practical.
3. The initial prototype may be AI-assisted. The final academic implementation must remain understandable and reproducible by the project team without relying on AI-generated code that the team cannot explain.
4. The user is a beginner and wants Antigravity to perform most file creation and coding, while also learning the purpose of the architecture, files, functions, database and code. Prefer clear, conventional Python and frontend code over clever abstractions.
5. Do not generate the entire application in one operation. Work in small milestones: inspect, plan, get approval, implement, test, explain changed files, and then prepare a Git checkpoint.
6. Do not commit or push to GitHub automatically. Ask for approval before Git commits or pushes.
7. Do not assume a requirement that is not specified. Mark unresolved details as **OPEN / TBD** and ask when the decision becomes necessary.

## B. Confirmed application structure and access

1. Keep the two access areas in the same application: a public member registration page and a protected administrator area.
2. The public registration page is intended for prospective members using their own phones. It collects information and a photograph, then submits an application with **Pending Approval** status. It must not reveal member records, the admin dashboard or any administrative operation.
3. The administrator reviews pending applications, can correct details, approves or declines/keeps pending as appropriate, assigns a trainer where required, and activates the membership. The exact decline workflow can be finalized during implementation.
4. Members do not have individual login accounts in Version 1. Trainers do not have separate login accounts in Version 1. Only the administrator has a protected login.
5. The public-facing homepage is a minimal landing page containing the gym identity and navigation to the available public/administrative entry points as appropriate. The dashboard is a separate admin page and must not be made the homepage.
6. Use separate route access controls and server-side authorization. Hiding admin links in the frontend is not sufficient protection.

## C. Member-management clarifications

1. A profile photograph is mandatory during registration, with clear consent for its storage and use in the member profile. The original uploaded photograph should be retained as needed for the portrait-processing workflow.
2. Gender is mandatory, with the three options in the original proposal: Male, Female and Non-binary.
3. Blood group is mandatory. Use the eight standard options listed in the original proposal. Do not add an “Unknown” option. Store blood group as a record only; do not use it to determine fitness plans, BMI remarks, trainer matching or other fitness decisions.
4. Record date of birth and calculate age automatically.
5. Keep initial height and weight as baseline/reference measurements, and record monthly follow-up measurements as separate historical fitness assessments rather than overwriting the baseline.
6. BMI may be calculated and shown with a neutral explanatory remark. It is informational only, not a diagnosis, should not be overemphasized, and must not determine trainer assignment. Use an appropriate age-based interpretation where relevant; do not apply adult-only interpretations indiscriminately.
7. Fitness-goal examples discussed include weight gain, weight loss, general fitness / “getting fit”, and professional training. The final list and wording of goal options remain **OPEN / TBD**.
8. Fitness level options remain Beginner, Intermediate and Advanced.
9. Preserve deactivated members and their historical memberships, payments, attendance and assessments. Do not hard-delete records as the normal workflow.
10. Search, filters, profile views and 7-day / 30-day membership-expiry alerts remain part of the member module.

## D. Trainer assignment clarifications

1. Automatic trainer recommendation/assignment is a signature feature and should be implemented using transparent, understandable Python rules (conditions, loops, lists/dictionaries and sorting), not complex machine learning.
2. Matching may consider member goal, fitness level, relevant trainer specialisation, selected morning/evening shift, trainer availability, maximum capacity and current workload.
3. Balance the workload between eligible trainers as evenly as practical. Do not assign beyond a trainer's configured maximum capacity.
4. Trainer experience and qualifications are profile information for display; they must **not** be numerical scoring factors in the assignment algorithm.
5. A member can have at most one assigned trainer at a time.
6. A trainer is not mandatory for every member. Retain the member's answer to whether a trainer is required; do not force an assignment when the member does not require one.
7. The gym schedule is Monday to Saturday, with Sunday as the weekly holiday. Do not collect or match individual preferred training days in Version 1.
8. Morning and evening training shifts are supported.
9. No automatic temporary substitute-trainer feature in Version 1.
10. Possible trainer specialisation labels discussed include newcomers/beginners, younger members, professionals and ladies/women. Treat the final taxonomy and its matching rules as **OPEN / TBD**; do not invent a rigid classification system.
11. The administrator should be able to review, confirm or manually change the suggested assignment.

## E. Membership, payment and attendance clarifications

1. Membership plans in the supplied proposal are Monthly (1 month), Quarterly (3 months), Half-yearly (6 months) and Annual (12 months). Keep plan duration configurable where practical, without adding unnecessary complexity.
2. Membership records and payment records are logically separate even if their functions appear together in the interface. Preserve renewal and payment history.
3. No integrated payment gateway or online payment processing. Supported recorded methods are Cash and UPI. The interface may display the gym's UPI QR image; an administrator manually confirms and records payment.
4. Payment status includes Paid, Pending and Partially Paid. Store member, amount, date, method and status.
5. Attendance must prevent duplicate active check-ins and invalid check-outs. Keep check-in, check-out, duration, daily history, member history, calendar and missing-check-out handling.

## F. Equipment and analytics clarifications

1. Equipment should be grouped by practical categories, including weights/accessories, machines and cable attachments.
2. Quantity-based equipment such as dumbbells must be recorded by weight/specification and quantity. Individual machines should be tracked separately so their own status and maintenance history can be retained.
3. Display consistent illustrations alongside equipment names where available. The illustration source/asset workflow can be decided later; do not delay core inventory functionality for artwork.
4. Keep Working, Under Maintenance and Out of Service statuses, equipment details, quantities, purchase date where known, last maintenance date and maintenance history.
5. Pandas is an important academic and functional requirement, not a token dependency. Use it meaningfully for filtering, sorting, grouping, aggregation, summaries and CSV/Excel exports from actual application records.
6. NumPy, Matplotlib and Seaborn should be used where they serve clear numerical or visualization needs. Do not add or use libraries artificially.

## G. Technology and architecture guidance

1. Main language: Python. Backend: Flask. Templates: Jinja. Frontend: HTML, CSS and JavaScript. Initial database: SQLite.
2. C++ is not required. Do not introduce React or another frontend framework without a specific, explained technical reason.
3. The user wants to learn SQL and database relationships. If SQLAlchemy is proposed, explain its benefits and trade-offs and continue teaching the underlying SQL; do not hide database concepts behind an ORM. The choice between direct `sqlite3` and SQLAlchemy is **OPEN / TBD** until the database design stage.
4. Keep the application modular. Do not put all routes, database operations, business logic and templates into one large file. Propose the folder structure before creating it.
5. Keep the application, database, uploaded photographs/processed portraits, and configuration/secrets separate enough that the server device can be changed without rewriting business logic.
6. Do not hard-code passwords, secret keys or machine-specific paths. Use environment/configuration settings appropriate to a local deployment.
7. Use server-side validation and safe handling of uploaded files. Keep member photographs and private records inaccessible to unauthorised users.

## H. Hosting and deployment — confirmed direction

### Initial deployment: self-hosted on the gym's local network

1. The normal planned server device is a laptop/computer kept at the gym. It runs the Flask application and acts as the local server.
2. The gym's existing Wi-Fi router connects the server computer and users' devices. Members can open the public registration page from their phones while connected to the gym network. The administrator can use the admin interface from the laptop or another browser-enabled device on that network.
3. This is a self-hosted local-network application. Do **not** deploy the initial version to Vercel or another public hosting platform. Do not assume a cloud host is part of Version 1.
4. The server computer and application process must remain running for the website to be reachable. If the computer is shut down or disconnected, the site will be unavailable to devices on the network; stored data remains on the server's storage.
5. The project should be device-independent: keep application code, database, uploaded media and configuration organised so the server hardware can potentially be changed later.
6. An Android phone may be explored as a temporary alternative server in a later experiment, but it is not the reliable primary deployment plan. Do not promise that Android will keep the server alive in the background; battery, heat, operating-system process management and network restrictions must be tested.
7. Public hosting should remain technically possible in the future, but it is not the initial deployment. Avoid choices that unnecessarily lock the application to one machine or local IP.
8. Zero-cost tools and existing gym equipment/network are priorities. Do not require a paid hosting subscription, new router purchase or paid API without explicit approval. Do not promise that a cloud free tier is permanent or unlimited.
9. During deployment testing, check whether the router's guest Wi-Fi isolates wireless clients from the server computer. If client isolation is enabled, phones may not be able to reach the local server; this may require router configuration or use of an appropriate staff/member network. Do not assume every router behaves the same.
10. A friendly local network name may be considered later, but do not promise that a name such as `gym.local` will work without checking the router/device name-resolution setup.
11. Before real-world use, plan secure admin access, safe local-network exposure, data backup and recovery. The exact backup procedure and router configuration remain **OPEN / TBD**.

## I. UI, visual design and frontend workflow — clarified and deliberately deferred

### The user owns the visual direction

1. The user wants personal control over the interface design and does not want a generic AI-generated website or the familiar, repetitive “AI dashboard” appearance. Do not invent a complete visual identity, colour palette, typography system, card style, icon style, gradients, animations or decorative design language.
2. The user will choose the visual direction, colour palette, typography, branding and overall look. The exact UI design is intentionally deferred until the functional structure is in place.
3. Canva may be used by the user for branding, visual references, assets or moodboards. Figma may be considered for detailed screen design. Google Stitch was discussed as an optional exploration tool, not a required dependency. These tools and the exact workflow are **OPEN / TBD**.
4. The user may provide screenshots, mockups, Canva exports or other visual assets. ChatGPT will help interpret the supplied design and translate it into precise implementation guidance; Antigravity will implement the approved HTML/CSS/JavaScript/Jinja changes. Do not replace the user's supplied design with an AI-generated alternative.
5. For the initial prototype, build **plain functional structure only**: routes, page hierarchy, forms, navigation, content areas and working interactions. Use minimal practical styling only where needed for readability, basic layout and responsive operation.
6. Do not spend time on the final colour palette, branding, decorative graphics, polished dashboard styling, elaborate transitions, animations or visual effects until the user explicitly begins the design phase.
7. The homepage remains a minimal landing page with gym name/navigation; the admin dashboard remains a separate page. Functional structure should be easy to restyle later without rewriting backend logic.

## J. AI tools and collaboration workflow

1. The primary day-to-day coding workspace is VS Code with the Google Antigravity extension. The separately installed Antigravity App remains available for broader agent/project management when useful; it is not necessary to perform every coding task in both interfaces. The user is not installing Antigravity Standalone IDE as a second editor.
2. The available long-term model for this workflow is **Gemini 3.8 Flash**, because the user's current plan does not provide the other discussed Gemini 4, Claude or GPT-OSS models. Do not design the workflow around model access the user does not have.
3. Use the repository documentation as durable context. Do not assume Antigravity can see or remember the user's ChatGPT conversation. Read `AGENTS.md`, `docs/PROJECT_BRIEF.md`, and `docs/DECISIONS.md` before substantial work.
4. Before significant work: inspect the repository, explain the objective, present a concise implementation plan and identify files to be changed. Wait for user approval before making multi-file or architectural changes.
5. After implementation: report changed files, explain important logic in beginner-friendly language, run relevant tests, describe their results honestly, and identify anything not completed.
6. Keep prompts and tasks bounded. Prefer one module or milestone at a time. Do not ask the model to generate the whole project in one giant operation.
7. ChatGPT's role is project planning, architecture guidance, prompt preparation, reviewing proposed changes, explaining code and helping translate the user's design into implementation requirements. Antigravity's role is the primary coding agent. The user makes product/design decisions, approves plans, tests the application and learns the implementation.

## K. Current development environment (as of 19 November 2026)

- Operating system: Windows 10, 64-bit.
- Project directory: `D:\GymManagementSystem`.
- Python: 3.15.2.
- pip: 26.2.2 at last recorded check.
- Flask: 3.1.3 installed in the project virtual environment.
- Git for Windows: 2.56.1.windows.1 at last recorded check.
- VS Code installed.
- Microsoft Python extension installed.
- Google Antigravity VS Code extension installed and signed in.
- Antigravity App installed and signed in.
- Project virtual environment: `.venv` (activated in the VS Code PowerShell terminal).
- Git repository initialised on branch `main`, connected to a private GitHub repository, and first commit pushed.
- `.gitignore` exists and excludes `.venv/`, Python cache files, `.env`, database files, `instance/` and `uploads/` as currently configured. Inspect the actual file before changing it.
- Existing `app/` folder and `app/__init__.py` were created during setup. Inspect the current file contents before assuming whether it is empty or already contains code.

## L. Immediate next milestone

1. Do not begin visual design. Do not build the full system yet.
2. First establish complete permanent documentation in the repository: `AGENTS.md`, `docs/PROJECT_BRIEF.md`, and `docs/DECISIONS.md`.
3. `docs/PROJECT_BRIEF.md` must preserve the full original proposal above, including all its module details and proposed database/Python concepts, and incorporate the later clarifications in this addendum. It may reorganise for readability, but it must not silently omit, shorten away or contradict any requirement. Where a later clarification supersedes an earlier statement, explicitly record that relationship.
4. `AGENTS.md` must instruct future agents to read the project brief and decisions before acting, follow the beginner-friendly approval workflow, and avoid unapproved UI design.
5. `docs/DECISIONS.md` must separate confirmed decisions, rejected/out-of-scope items and genuinely open decisions. Do not turn suggestions into confirmed decisions.
6. Before creating these files, inspect the existing repository and present the proposed plan. Do not modify existing application code, install packages or run unnecessary commands during the documentation-planning step.
7. After the documentation is approved and created, the first implementation milestone is a plain, minimally styled, working Flask site skeleton. Focus on application structure, routes, templates and basic navigation only. Do not design the final visual interface.
