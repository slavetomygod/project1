# SYSTEM SPECIFICATION REPORT
## PROJECT: RESTRICTED MEDICAL APPOINTMENT APPLICATION ARCHITECTURE
### CLIENT DELIVERABLE | STRUCTURAL BLUEPRINT & FUNCTIONAL SPECIFICATION

---

## 1. PROJECT METADATA & COMPILATION OVERVIEW
* **System Type:** Hybrid Medical Portal (Decoupled Front-End / Centrally Managed Python API Backend)
* **Target Audience Base:** Public Patients (Open Access Track) vs. Accredited Medical Practitioners (Token-Restricted Access Track)
* **Data Layer Topology:** Centralized SQL Relational Storage Model via Object-Relational Mapping (ORM) System
* **Network Infrastructure Pattern:** Front-end assets send payloads via standard asynchronous HTTP API client methods straight to a secure network endpoint controller managed by Python execution pipelines.

---

## 2. CENTRALIZED FILE MANAGEMENT DIRECTORY
```text
hospital-booking-app/
│
├── backend/                        # Central Python Server Logic (FastAPI / Flask Engine)
│   ├── database/
│   │   ├── __init__.py             # Namespace Package Anchor
│   │   ├── connection.py           # Database Transaction Piping Manager
│   │   └── models.py               # SQL Row-to-Column Structural Mappings
│   │
│   ├── routes/
│   │   ├── auth.py                 # Authorization Systems Controller
│   │   ├── appointments.py         # Scheduling Matrix Routing Engine
│   │   ├── reviews.py              # Statistical Metric Analyzer
│   │   └── chat.py                 # Automated Natural Language Pipeline
│   │
│   └── main.py                     # Primary Core Entry Execution Frame
│
├── frontend/                       # Presentation layer split to insulate individual UI logic
│   ├── css/                        # Isolated View Stylesheets
│   │   ├── patient/
│   │   │   ├── home.css            # Styles landing, open logins, chat frame grids
│   │   │   ├── profile.css         # Typography layouts for demographic form fields
│   │   │   ├── book.css            # Matrix layouts for calendar blocks and selectors
│   │   │   ├── history.css         # Grid system handling timeline visual markers
│   │   │   └── reviews.css         # Structural view formatting for metrics data
│   │   │
│   │   └── doctor/
│   │       ├── invite-only.css     # Clean onboarding card elements
│   │       ├── login.css           # Isolated administration gate layout rules
│   │       ├── requests.css        # Interactive triage status tracker styling
│   │       ├── shift.css           # Hour-block spreadsheet grid framework layout
│   │       └── profile.css         # Credential form presentation management rules
│   │
│   ├── js/
│   │   └── api.js                  # Asynchronous Network Call Controller (Frontend Interface Engine)
│   │
│   └── templates/                  # Structural Document Blueprints (Decoupled HTML Fragments)
│       ├── patient/
│       │   ├── home.html           # Onboarding view container containing main automated live chat frame
│       │   ├── profile.html        # Verified clinical identity validation matrix
│       │   ├── book.html           # Multi-step medical slot reservation panel
│       │   ├── history.html        # Interactive chronological archive grid
│       │   └── reviews.html        # Public rating aggregated statistics panel
│       │
│       └── doctor/
│           ├── invite-only.html    # Guarded signature account creation terminal
│           ├── login.html          # Secondary internal staff authorization gate
│           ├── requests.html       # Pending action logs dashboard
│           ├── shift.html          # Dynamic hour roster and historical patient index tracker
│           └── profile.html        # Secured physician credentials dashboard
│
├── .env                            # Hidden Host Environment Vault File
├── .gitignore                      # Security Restrict Tracking Document List
└── requirements.txt                # System Packages Dependency Manifest
```

---

## 3. FRONTEND VISUAL INTERFACE & FUNCTIONAL ASSIGNMENTS

### A. PATIENT WEB INTERFACE DOMAIN

#### 1. Page Template: `patient/home.html` | Stylesheet Path: `css/patient/home.css`
*   **Structural Scope:** Serves as the open public storefront landing layout. Features welcoming landing text, standard public user sign-in forms, and an immediate floating chatbot console layout.
*   **Offered Functions & Operational Hooks:**
    *   `login_with_email()`: Formats form inputs into serialized payloads to execute client identity validation checks.
    *   `login_with_google()`: Triggers public Single Sign-On authenticators via secure identity provider scopes.
    *   `send_chat_message()`: Extracts plain text arguments from browser forms to pass downstream via API pipelines.
    *   `stream_bot_response()`: Appends automation replies inside the interface window.

#### 2. Page Template: `patient/profile.html` | Stylesheet Path: `css/patient/profile.css`
*   **Structural Scope:** Confidential workspace managing basic personal information fields. Eliminates custom usernames, relying strictly on legal name variables to ensure verified medical record mapping.
*   **Offered Functions & Operational Hooks:**
    *   `save_profile_data()`: Gathers validated form parameters to execute backend demographic insertion records.
    *   `load_existing_profile()`: Hydrates interface inputs by retrieving profile history records from the system.

#### 3. Page Template: `patient/book.html` | Stylesheet Path: `css/patient/book.css`
*   **Structural Scope:** Guided medical scheduling utility layout. Prompts diagnostic illness evaluations, matches parameters to clinical specializations, and opens calendar hour selectors.
*   **Offered Functions & Operational Hooks:**
    *   `select_patient_target()`: Configures systemic data flags separating primary profile owners from family dependents.
    *   `filter_doctors_by_specialty()`: Requests tailored physician indexes filtered by illness domain attributes.
    *   `check_available_dates()`: Disables conflicting date options depending on working shift matrices.

#### 4. Page Template: `patient/history.html` | Stylesheet Path: `css/patient/history.css`
*   **Structural Scope:** Personal tracking archive. Renders chronological summaries displaying target dates, hours, and physician identities.
*   **Offered Functions & Operational Hooks:**
    *   `render_calendar_appointments()`: Plots historically saved appointments across calendar blocks.
    *   `request_appointment_cancellation()`: Alters targeted database entry status keys to canceled states.

#### 5. Page Template: `patient/reviews.html` | Stylesheet Path: `css/patient/reviews.css`
*   **Structural Scope:** Public transparency center. Displays overall service operation parameters alongside cached physician scores.
*   **Offered Functions & Operational Hooks:**
    *   `fetch_overall_service_scores()`: Pulls general staff and hospital metric feedback tallies.
    *   `fetch_doctor_star_averages()`: Displays mathematical calculations optimized by server data summaries.

---

### B. RESTRICTED MEDICAL PRACTITIONER PORTAL DOMAIN

#### 1. Page Template: `doctor/invite-only.html` | Stylesheet Path: `css/doctor/invite-only.css`
*   **Structural Scope:** Hidden registry dashboard completely blocked from structural navbars. Accessible only to incoming medical staff via unique token parameters embedded in URLs.
*   **Offered Functions & Operational Hooks:**
    *   `verify_invitation_token()`: Parses current browser link segments to evaluate active token arrays.
    *   `create_doctor_account()`: Collects new secure registration profiles to execute database insertion routines.

#### 2. Page Template: `doctor/login.html` | Stylesheet Path: `css/doctor/login.css`
*   **Structural Scope:** Isolated authentication portal. Keeps hospital staff authorization lines completely separate from patient routes.
*   **Offered Functions & Operational Hooks:**
    *   `authenticate_doctor_session()`: Submits staff identification keys to acquire dynamic session token headers.

#### 3. Page Template: `doctor/requests.html` | Stylesheet Path: `css/doctor/requests.css`
*   **Structural Scope:** Incoming queue dashboard. Displays real-time request metrics submitted by patients seeking help for specific illnesses.
*   **Offered Functions & Operational Hooks:**
    *   `approve_booking_request()`: Updates row status flags to move bookings into confirmed schedules.
    *   `reject_and_trigger_cascade()`: Rejects a slot request and initiates automatic rerouting to alternate specialists.

#### 4. Page Template: `doctor/shift.html` | Stylesheet Path: `css/doctor/shift.css`
*   **Structural Scope:** Internal timetable interface tracking practitioner schedules, daily work shifts, and confirmed patient time blocks.
*   **Offered Functions & Operational Hooks:**
    *   `load_daily_shift_hours()`: Populates timelines using pre-selected active daily blocks.
    *   `view_patient_medical_history()`: Displays historical clinical notes linked to incoming patients.

#### 5. Page Template: `doctor/profile.html` | Stylesheet Path: `css/doctor/profile.css`
*   **Structural Scope:** Certified configuration profile management interface. Stores qualifications, bio segments, and active performance review statistics.
*   **Offered Functions & Operational Hooks:**
    *   `update_medical_qualifications()`: Transmits credential updates and profile images to active server directories.
    *   `fetch_personal_review_metrics()`: Populates user dashboard views with cached system score matrices.

---

## 4. ASYNCHRONOUS FRONTEND INTERFACE ENGINE (`frontend/js/api.js`)
*   **Structural Scope:** Serves as the single source of truth for all browser network transactions. Completely replaces inline logic, standardizing communication protocols between front-end views and the Python runtime.
*   **Offered Functions & Operational Hooks:**
    *   `async handle_http_request(endpoint, method, payload)`: Universal execution handler that processes request configurations, sets token authorization headers, and processes JSON payloads safely.
    *   `async submit_patient_booking(booking_details)`: Captures multi-stage scheduling form vectors and fires payloads directly to the Python backend.
    *   `async transmit_chat_interaction(user_message)`: Routes chatbot inputs to backend processing engines, handling user text and appending bot responses safely.
    *   `async update_doctor_triage_decision(appointment_id, decision_type)`: Sends clinician approvals or rejections to backend routing endpoints, triggering cascade updates instantly when rejections occur.

---

## 5. BACKEND ENGINE ARCHITECTURE (PYTHON / SQL DATA SYSTEMS)

### A. DATABASE LAYER ARCHITECTURE

#### 1. Configuration Script: `backend/database/connection.py`
*   **Structural Scope:** Instantiates operational connection strings using modern Object-Relational Mapping (ORM) environments. Integrates configuration variables safely from hidden runtime environment files.
*   **Offered Functions & Operational Hooks:**
    *   `initialize_database_engine()`: Boots the physical storage engine and tests credentials using configuration strings.
    *   `get_db_session()`: Generator loop providing thread-safe database transaction connections to backend modules.

#### 2. Configuration Script: `backend/database/models.py`
*   **Structural Scope:** Formal data structure definition file. Declares system relationships, primary key constraints, and database indices.
*   **Offered Functions & Operational Hooks:**
    *   `Class User(Base)`: Maps fundamental attributes like full name strings, security hashes, role enums, age integers, and gender characters.
    *   `Class DoctorProfile(Base)`: Links practitioner profiles directly to user accounts, adding qualification notes and cached performance fields.
    *   `Class Appointment(Base)`: Manages core scheduling data records, tracking date values, status strings, and diagnostic tags.
    *   `Class Review(Base)`: Formats evaluation records, connecting review comments and star indexes to corresponding appointment fields.

---

### B. SYSTEM FUNCTIONAL ROUTING PATHWAYS

#### 1. Endpoint Module: `backend/routes/auth.py`
*   **Structural Scope:** Controls access security for all users. Validates patient sessions openly while strictly locking doctor creation flows via verification engines.
*   **Offered Functions & Operational Hooks:**
    *   `register_public_patient()`: Validates registration fields, hashes passwords, and appends new patient records.
    *   `validate_invitation_token()`: Confirms administrative invitation links, locking account creation if strings are invalid.
    *   `generate_access_token()`: Encrypts identification criteria to issue cryptographically signed session tokens.

#### 2. Endpoint Module: `backend/routes/appointments.py`
*   **Structural Scope:** Central scheduler engine. Coordinates slot calculations, manages provider time grids, and handles automated cascade adjustments.
*   **Offered Functions & Operational Hooks:**
    *   `query_available_slots()`: Cross-checks scheduling tables with provider availability to calculate free appointment hours.
    *   `process_cascade_reroute()`: Reallocates an appointment request to available alternative specialists if the original clinician rejects the slot.

#### 3. Endpoint Module: `backend/routes/reviews.py`
*   **Structural Scope:** Analytical processing node. Manages user satisfaction metrics and updates cached score entries to prevent slow database queries.
*   **Offered Functions & Operational Hooks:**
    *   `commit_new_review()`: Inserts evaluation records into relational review tables.
    *   `recalculate_doctor_rating_average()`: Runs database queries to aggregate stars and update performance columns.

#### 4. Endpoint Module: `backend/routes/chat.py`
*   **Structural Scope:** Python logic controller powering the chatbot interface. Evaluates patient inputs, handles immediate support requests, and flags intents that require human clinical scheduling.
*   **Offered Functions & Operational Hooks:**
    *   `evaluate_chat_intent()`: Scans user messages for scheduling keywords to route users directly to booking workflows.
    *   `log_chat_history()`: Records conversation parameters into persistent audit logging tables.

#### 5. Main Framework App Entry: `backend/main.py`
*   **Structural Scope:** Main initialization pipeline. Configures routing paths, sets up security rules, and starts server processes.
*   **Offered Functions & Operational Hooks:**
    *   `bootstrap_application()`: Binds data schemas, configures security allowances, and attaches subsystem routers into a single engine instance.

---
*This is for informational purposes only. For medical advice or diagnosis, consult a professional. AI responses may include mistakes.*
