# GYM MANAGEMENT SYSTEM — COMPREHENSIVE PROJECT SPECIFICATION
### Document: `docs/PROJECT_BRIEF.md`

This document serves as the permanent, comprehensive single source of truth for the **Gym Management System**. It contains the complete, unedited original project proposal preserved verbatim, followed by the complete set of confirmed later decisions, architectural specifications, and implementation guidelines.

---

# TABLE OF CONTENTS
1. [Part 1: Master Specification — Original Proposal (Verbatim)](#part-1-master-specification--original-proposal-verbatim)
   - [1. Project Overview](#1-project-overview)
   - [2. Technology Stack](#2-technology-stack)
   - [3. Application Structure and Access](#3-application-structure-and-access)
   - [4. Main Application Modules](#4-main-application-modules)
     - [Module 1: Member Management & Illustrated Portraits](#module-1-member-management)
     - [Module 2: Trainer Management & Recommendation](#module-2-trainer-management)
     - [Module 3: Membership and Payment Management](#module-3-membership-and-payment-management)
     - [Module 4: Attendance Management](#module-4-attendance-management)
     - [Module 5: Equipment Management](#module-5-equipment-management)
     - [Module 6: Reports and Data Analytics](#module-6-reports-and-data-analytics)
   - [5. Proposed Database](#5-proposed-database)
   - [6. Python Concepts Demonstrated](#6-python-concepts-demonstrated)
   - [7. Scope Boundaries](#7-scope-boundaries)
   - [8. Development Philosophy](#8-development-philosophy)
2. [Part 2: Confirmed Decisions, Clarifications & Implementation Architecture](#part-2-confirmed-decisions-clarifications--implementation-architecture)
   - [A. Authority and Relationship to Original Proposal](#a-authority-and-relationship-to-original-proposal)
   - [B. Scope, Scale and Educational Objectives](#b-scope-scale-and-educational-objectives)
   - [C. Application Structure, Entry Points & Route Security](#c-application-structure-entry-points--route-security)
   - [D. Member Management & Illustrated Portrait Pipeline](#d-member-management--illustrated-portrait-pipeline)
   - [E. Trainer Management & Transparent Assignment Logic](#e-trainer-management--transparent-assignment-logic)
   - [F. Membership, Payment & Attendance Workflows](#f-membership-payment--attendance-workflows)
   - [G. Equipment Tracking & Maintenance Workflow](#g-equipment-tracking--maintenance-workflow)
   - [H. Practical Academic Data Analytics (Pandas, NumPy, Matplotlib, Seaborn)](#h-practical-academic-data-analytics-pandas-numpy-matplotlib-seaborn)
   - [I. Technology Stack & Database Strategy](#i-technology-stack--database-strategy)
   - [J. Hosting & Deployment Strategy (Local Wi-Fi Network Hosting)](#j-hosting--deployment-strategy-local-wi-fi-network-hosting)
   - [K. UI/UX Ownership & Frontend Design Workflow](#k-uiux-ownership--frontend-design-workflow)
   - [L. Tooling, Environment & AI Workflow](#l-tooling-environment--ai-workflow)
   - [M. Cross-Reference: Later Clarifications vs. Original Proposal](#m-cross-reference-later-clarifications-vs-original-proposal)

---

# PART 1: MASTER SPECIFICATION — ORIGINAL PROPOSAL (VERBATIM)

*The text in this section is preserved exactly as written in the original proposal (`GymManagementSystem_MasterSpecification.md`). It has not been shortened, paraphrased, or modified.*

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

# PART 2: CONFIRMED DECISIONS, CLARIFICATIONS & IMPLEMENTATION ARCHITECTURE

---

## A. Authority and Relationship to Original Proposal

1. **Preservation:** The complete Version 1 proposal in Part 1 is preserved verbatim. No requirement has been deleted or silently removed.
2. **Authority:** This Part 2 incorporates all subsequent agreements, decisions, and technical clarifications. Where a confirmed decision in Part 2 updates, sharpens, or overrides a statement from Part 1, the decision in Part 2 is authoritative.
3. **Traceability:** Every modification and clarification is explicitly documented in Section M below and in `docs/DECISIONS.md`.

---

## B. Scope, Scale and Educational Objectives

1. **Single Gym Only:** The application manages operations for **one gym only**. Even if the business operates multiple real-world branches, this system will not model or manage multiple locations.
2. **Educational & Academic Focus:**
   - The user is a beginner learning programming and database engineering.
   - Code must be clear, transparent, well-commented, and easily explained in an academic project viva or presentation.
   - Avoid "magical" abstractions, obscure decorators, or complex third-party libraries where standard Python, Flask, and SQL suffice.
3. **Modular Delivery:**
   - Build in small, verified milestones: Navigation & Structure $\rightarrow$ Database & Models $\rightarrow$ Core Workflows $\rightarrow$ Analytics & Reporting $\rightarrow$ Special Features.
   - Modules must remain sufficiently independent so that specific components can be demonstrated or adjusted without breaking the entire application.

---

## C. Application Structure, Entry Points & Route Security

1. **Two Core Application Areas:**
   - **Public Area:** Minimal landing page and public member self-registration.
   - **Protected Admin Area:** Complete administration panel for gym staff.
2. **Landing Page vs. Admin Dashboard Separation:**
   - The **public landing page** is a minimal page presenting the gym identity and links to:
     - Member Registration Form (public)
     - Admin Login Form (protected)
   - The **Admin Dashboard** is a separate, protected interface displaying operational tools, member lists, and summaries. The dashboard must **never** be the default homepage.
3. **Member Self-Registration Flow:**
   - Prospective members open the registration page on their mobile phones while connected to the gym's local Wi-Fi.
   - The form collects personal info, contact info, health measurements, fitness goals, trainer needs, and an uploaded photo.
   - Upon submission, the record is assigned status **`Pending Approval`**.
   - The public form provides a clear confirmation message to the user and immediately ends the public flow; it **never** exposes existing member records, other applications, or any administrative functions.
4. **Admin Approval Workflow:**
   - The administrator logs in, reviews pending applications in an approval queue, verifies information, and makes corrections if necessary.
   - If trainer assistance was requested, the admin reviews the system's recommended trainer (or selects another) and assigns them.
   - **Payment Confirmation vs. Membership Activation `[OPEN / TBD]`:** The administrator records or confirms payment details (Cash or UPI). The system must **not** assume that a membership must always be fully paid before activation; the exact operational relationship between payment status (`Paid`, `Pending`, or `Partially Paid`) and membership status transition to `Active` is marked `[OPEN / TBD]` and will be finalized during workflow design.
   - The exact workflow for declining, rejecting, or keeping an application pending is marked `[OPEN / TBD]`.
5. **Route Security & Server-Side Authorization:**
   - Admin routes must be protected using server-side session authentication.
   - Simply hiding admin buttons or links in HTML templates is strictly insufficient. Unauthorized requests to `/admin/*` routes must be redirected to the login page with an appropriate message.

---

## D. Member Management & Illustrated Portrait Pipeline

1. **Mandatory & Specific Fields:**
   - **Profile Photograph:** Mandatory during registration. Clear user consent for storage and profile use must be displayed on the form. Original raw images must be securely stored.
   - **Gender:** Mandatory field with exactly three options: `Male`, `Female`, and `Non-binary`.
   - **Blood Group:** Mandatory field with exactly eight standard medical options: `A+`, `A-`, `B+`, `B-`, `AB+`, `AB-`, `O+`, and `O-`. Do **not** include an "Unknown" option. Blood group is strictly a medical/emergency record; it must **never** be used to determine fitness routines, BMI remarks, or trainer matching.
   - **Date of Birth & Age:** Date of birth is stored; age is automatically calculated via Python/JavaScript date logic.
2. **Baseline vs. Historical Fitness Assessments:**
   - The initial height and weight recorded during registration are permanently retained as the member's **baseline reference measurements**.
   - Monthly progress measurements are recorded in a separate `fitness_assessments` table, preserving full historical tracking over time rather than overwriting baseline records.
   - **BMI:** Calculated from height and weight ($BMI = \frac{\text{weight in kg}}{(\text{height in m})^2}$). A neutral, age-appropriate remark may be displayed. BMI is strictly informational and must **never** be used for trainer assignment or medical diagnosis.
3. **Fitness Goals & Levels:**
   - **Fitness Level:** `Beginner`, `Intermediate`, and `Advanced`.
   - **Fitness Goals:** Example goals discussed include `Weight gain`, `Weight loss`, `Being fit / general fitness`, and `Professional training`. The exact final dropdown list is marked `[OPEN / TBD]`.
4. **Soft Deactivation Rule:**
   - Gym members are deactivated (`status = 'Inactive'`), never hard-deleted from the database during normal operations.
   - Deactivated members are excluded from active workload tallies and active member counts, but all their historical records (previous memberships, payments, attendance, and fitness logs) remain intact.
5. **Expiration Alerts:**
   - The **Admin Dashboard / Member Management section** must highlight memberships expiring within the next 7 days and next 30 days for renewal follow-up (members do not have individual login accounts).
6. **Illustrated Member Portrait Feature (Special Feature):**
   - **Desired Functional Result:** Standardized, clean, polished digital illustrated portraits of each member placed against a selected plain-colour background, providing visual consistency across profile pictures instead of displaying unrelated raw photographs. Comic, sketch, and 3D avatar styles are explicitly excluded.
   - **Experimental Processing Techniques & Proposed Tools:** The original specification proposes local image processing using **MediaPipe** for person background segmentation, **OpenCV** for artistic digital filtering (smoothing, color quantization), and **Pillow** for cropping, resizing, and compositing over a solid plain-color background.
   - **Clear Technical Distinction & Early POC:** The desired functional outcome is an important proposed feature of the system. However, the specific image-processing techniques and proposed Python libraries are experimental. Because third-party libraries (such as MediaPipe and OpenCV wheels) can present compatibility challenges across newer Python releases (including Python 3.15 on 64-bit Windows), this feature will undergo an **early Proof of Concept (POC)** to evaluate technical feasibility, installation stability, and visual output quality before being wired into the core member registration workflow.

---

## E. Trainer Management & Transparent Assignment Logic

1. **Assignment Algorithm Philosophy:**
   - Must be implemented using **pure, transparent Python logic** (`if`/`else` conditions, loops, list/dictionary lookups, and sorting).
   - Machine learning algorithms, neural networks, or black-box weighted scoring systems are strictly prohibited.
2. **Matching Criteria:**
   When a member requests a trainer, the recommendation engine evaluates active trainers based on:
   - **Specialization Match:** Trainer's coaching specialty aligns with the member's fitness goal.
   - **Member Fitness Level:** The member's own fitness level (Beginner, Intermediate, Advanced) is collected and may be used when matching against an explicitly defined trainer specialization (such as coaching beginners/newcomers), if such a category is approved later.
   - **Shift Availability:** Trainer works the member's preferred shift (`Morning` or `Evening`).
   - **Active Capacity:** Trainer's current assigned count is strictly below their configured `max_capacity`.
   - **Workload Balancing:** Eligible trainers meeting the criteria are ranked, prioritizing the trainer with the lowest current workload (lowest active members or lowest assigned percentage).
3. **Display-Only Trainer Profile Information (Strictly Non-Scoring):**
   - The trainer's experience level, years of experience, qualifications, and certifications are profile display fields only.
   - They must **never** influence trainer assignment, mathematical scoring, or workload ranking.
4. **Assignment Constraints:**
   - **Maximum One Trainer:** A member may have at most one assigned trainer at any given time.
   - **Trainer is Optional:** A member can choose not to request a trainer. If "No" is selected, no trainer is assigned.
   - **Admin Override:** The system provides a recommendation; the administrator has the final authority to accept the recommendation or manually choose another trainer.
5. **Operating Schedule:**
   - Monday through Saturday operations; Sunday is a weekly holiday.
   - Morning and Evening shifts.
   - Version 1 does not model or match individual preferred training days.
   - No automatic temporary substitute trainer logic in Version 1.
6. **Open Taxonomies:**
   - Trainer specialisation labels discussed as examples include **newcomers**, **younger members**, **professionals**, and **ladies**. The final speciality taxonomy and its mapping to member fitness goals remain `[OPEN / TBD]`; no rigid classification system should be invented in advance.

---

## F. Membership, Payment & Attendance Workflows

1. **Membership Plans:**
   - Standard durations: Monthly (1 month), Quarterly (3 months), Half-yearly (6 months), and Annual (12 months).
   - System automatically calculates expiry dates based on the start date and plan duration.
   - Membership renewal must append a new record to membership history, never overwrite previous periods.
2. **Payments & Manual Verification:**
   - **Zero Payment Gateway Integration:** No Stripe, Razorpay, or online card processing.
   - Supported payment methods: **Cash** and **UPI**.
   - The admin interface can display the gym's UPI QR code image to facilitate payments.
   - The administrator manually enters and confirms payments.
   - Payment status values: `Paid`, `Pending`, or `Partially Paid`.
   - **Relationship to Membership Activation `[OPEN / TBD]`:** The system records payments, but does not enforce a rigid rule that a membership can only be activated when payment is fully paid. Rules for handling members with pending or partial payments during activation will be resolved during workflow design.
   - Payment records and membership records are stored in separate, relational database tables.
3. **Attendance Tracking:**
   - Records check-in time, check-out time, and automatically calculates duration of visit.
   - **Integrity Rules:**
     - Prevent duplicate active check-ins (a member cannot check in twice without checking out).
     - Prevent invalid check-outs (cannot check out without an active check-in).
     - Flag missing check-outs (visits left open past operating hours).
   - Provide daily attendance rosters, member-specific visit history, and a monthly calendar visualization.

---

## G. Equipment Tracking & Maintenance Workflow

1. **Categories:**
   - **Weights & Accessories:** Dumbbells, weight plates, barbells, EZ curl bars, kettlebells.
   - **Machines:** Treadmills, exercise bikes, leg press, chest press, cable crossover machines.
   - **Cable Attachments:** Straight bars, tricep ropes, V-handles, ankle straps.
2. **Tracking Strategy:**
   - **Quantity-Based Inventory:** Items such as dumbbells and weight plates are tracked by weight specification and total quantity.
   - **Serialized Unit Tracking:** Major machines are tracked as individual units with unique IDs to preserve individual repair and maintenance logs.
3. **Statuses:**
   - Each item or machine is marked as `Working`, `Under Maintenance`, or `Out of Service`.
4. **Maintenance Logging:**
   - Record maintenance date, description of work, and equipment status.
   - Additional fields such as maintenance cost and technician details are optional/open fields `[OPEN / TBD]` rather than confirmed mandatory requirements.
5. **Visual Identification:**
   - Consistent illustrations or visual icons will accompany equipment names to facilitate fast visual inventory. Asset sources are marked `[OPEN / TBD]`.

---

## H. Practical Academic Data Analytics (Pandas, NumPy, Matplotlib, Seaborn)

These libraries represent core academic requirements and must be used meaningfully on real database records rather than imported cosmetics:

1. **Pandas:**
   - Read SQLite tables into DataFrames (`pd.read_sql_query`).
   - Grouping, filtering, and aggregation:
     - Member demographic summaries (age distributions, gender ratios).
     - Membership revenue summaries and plan popularities.
     - Trainer workload distributions.
     - Attendance frequencies and peak visiting hours.
   - Export structured reports to downloadable **CSV** and **Excel** files.
2. **NumPy:**
   - Compute mathematical and statistical measures:
     - Mean, median, min, max, and standard deviation of daily attendance.
     - Statistical distributions of member visit durations.
     - BMI and fitness assessment statistical metrics.
3. **Matplotlib & Seaborn:**
   - Generate static charts and statistical plots rendered into images or embedded in admin reports:
     - Monthly membership growth trends.
     - Attendance heatmaps (day-of-week vs. hour-of-day).
     - Trainer workload comparison bar charts.
     - Equipment operational status pie/donut charts.
     - Revenue collection breakdowns.

---

## I. Technology Stack & Database Strategy

1. **Languages & Core Frameworks:**
   - **Language:** Python 3.15.2
   - **Backend:** Flask 3.1.3
   - **Template Engine:** Jinja2
   - **Frontend:** Standard HTML5, CSS3, vanilla JavaScript.
   - **Frameworks:** No heavy frontend frameworks (React, Angular, Vue) are permitted.
2. **Database:**
   - **Primary Engine:** SQLite.
   - **Schema Tables (11 planned):**
     1. `members`
     2. `trainers`
     3. `membership_plans`
     4. `membership_records`
     5. `payments`
     6. `attendance`
     7. `equipment`
     8. `equipment_maintenance`
     9. `fitness_assessments`
     10. `trainer_assignments`
     11. `trainer_availability`
   - **Database Access Choice (`[OPEN / TBD]`):**
     The owner is learning SQL and relational database structures. The choice between raw `sqlite3` queries and `Flask-SQLAlchemy` will be made during the database design milestone. If an ORM like SQLAlchemy is used, it must be accompanied by explanations of the underlying SQL queries so that database learning is not obscured.
3. **Zero-Cost Dependency Rule:**
   - No paid cloud APIs, services, or tools will be introduced without prior explicit approval.

---

## J. Hosting & Deployment Strategy (Local Wi-Fi Network Hosting)

1. **Primary Deployment Model:**
   - **Server Hardware:** The gym owner's laptop/PC located at the gym.
   - **Application Execution:** Runs the Flask server locally.
   - **Network Connectivity:** Connected to the gym's existing Wi-Fi router.
   - **User Access:**
     - Members access the public registration form from their smartphones while connected to the gym Wi-Fi.
     - The administrator accesses the admin panel from the laptop itself (via `localhost`) or from another authorized device on the gym network.
2. **Public Cloud Hosting Status:**
   - Public cloud hosting (Vercel, Render, AWS, Heroku, etc.) is **deferred for Version 1**.
   - Cloud hosting is **not permanently rejected**; application architecture and configuration will remain modular and portable so the project can be deployed to a cloud server in the future without rewriting core logic.
3. **Android Phone Server Status:**
   - Experimenting with running the server on an Android phone is an **optional future exploration**, not the primary deployment plan.
4. **Network & Router Considerations:**
   - **Server Availability:** The laptop must remain powered on and running Flask for the application to be accessible. Application data is persisted locally on the server computer, while backup and recovery arrangements remain `[OPEN / TBD]`.
   - **Wi-Fi Client Isolation:** Gym routers with guest Wi-Fi enabled often feature "Client Isolation" (which prevents wireless devices from communicating with other devices on the same network). During local deployment testing, the router configuration must be verified to ensure phones can communicate with the server laptop's local IP address.
   - **Local IP / Hostname:** Addressing will initially use the server's local network IP address (e.g., `http://192.168.1.50:5000`). Setting up a friendly local network name (like `http://gym.local`) is marked `[OPEN / TBD]`.
   - **Backup & Recovery:** Local backup strategies for the SQLite database file and uploaded member images are marked `[OPEN / TBD]`.

---

## K. UI/UX Ownership & Frontend Design Workflow

1. **Sole Visual Ownership:**
   - The project owner retains **100% exclusive control** over all visual design decisions:
     - Color palettes
     - Typography and fonts
     - Branding and logos
     - Screen layouts and component hierarchy
     - Visual graphics and iconography
2. **No AI-Generated Themes:**
   - AI coding agents must **never** invent arbitrary visual themes, colorful cards, gradient backgrounds, or boilerplate dashboard aesthetics.
3. **Staged Frontend Workflow:**
   - **Phase 1 (Current):** Build **plain, functional HTML structures** only. Use clean forms, data tables, simple buttons, and semantic HTML elements. Minimal CSS is permitted only where necessary for readability, basic spacing, and responsive layout.
   - **Phase 2 (Design Phase):** The owner will create visual concepts and references using tools of their choice (such as **Canva**, **Figma**, or **Google Stitch** — all of which are optional exploration tools).
   - **Design Translation Pipeline:** The owner may use **ChatGPT** to review visual designs and translate them into precise implementation instructions. Antigravity will then implement the approved CSS, Jinja templates, and layouts.

---

## L. Tooling, Environment & AI Workflow

1. **Development Environment:**
   - Primary coding editor: **VS Code** with the **Google Antigravity** extension.
   - Broader agent management: **Antigravity App** (used when helpful for managing multi-agent tasks).
   - Preferred Model: **Gemini 3.8 Flash**, aligned with the user's available plan. Code and architecture must remain standard and reproducible, never relying on model-specific idiosyncrasies.
2. **Collaboration Principles:**
   - Inspect workspace before acting.
   - Present detailed implementation plans before making changes.
   - Wait for explicit user approval before touching code.
   - Provide beginner-friendly explanations of every file, function, and database table created.
   - Never commit or push to Git without approval.

---

## M. Cross-Reference: Later Clarifications vs. Original Proposal

The following table explicitly documents where later decisions clarify, refine, or update earlier statements in the original proposal:

| Topic | Original Proposal (Part 1) | Confirmed Later Decision (Part 2) | Nature of Update |
|---|---|---|---|
| **Gym Branches** | Listed "Multiple gym branches" under Scope Boundaries. | Strictly models **one single gym**; real-world branches are not modeled in software. | **Clarified & Affirmed** |
| **Landing Page vs Dashboard** | "A statistics-heavy dashboard will not be the homepage in Version 1." | Public homepage is a **minimal landing page**; Admin Dashboard is a separate, protected route. | **Clarified & Strictly Enforced** |
| **User Logins** | Members have no login; Admin has secure login; Trainers not mentioned. | **Administrator only** has a login. Neither members nor trainers have login accounts in Version 1. | **Clarified & Confirmed** |
| **Registration Status** | Member registers; admin manages/approves. | Submissions start with status **`Pending Approval`**; admin reviews queue to activate. | **Operational Flow Defined** |
| **Trainer Experience & Qualifications** | Included in trainer profile information. | Profile display fields only; **strictly prohibited** as numerical scoring factors in matching. | **Clarified & Restrained** |
| **Trainer Assignment Option** | Automated suggestion based on member criteria. | Member can opt out of trainer; **maximum 1 trainer** per member; workload balanced across eligible trainers. | **Rules Formalized** |
| **Hosting Strategy** | Silent on specific hosting infrastructure. | **Local Wi-Fi hosting** on owner's laptop. Cloud hosting deferred for V1 (but architecture kept portable). | **New Concrete Strategy** |
| **UI / Visual Design** | Emphasized functional application over visual appearance. | Owner has **complete personal visual control**. AI must build plain functional HTML first; no AI themes. | **Ownership Clarified** |
| **Illustrated Portraits** | Proposed MediaPipe, OpenCV, Pillow pipeline. | Retained as a key feature, but marked as requiring an **early Proof of Concept (POC)** for feasibility. | **Risk-Managed Strategy** |
| **Database Access Library** | Specified SQLite. | SQLite confirmed; choice between raw `sqlite3` and `Flask-SQLAlchemy` is **OPEN / TBD** to preserve SQL learning. | **Open Decision Documented** |
