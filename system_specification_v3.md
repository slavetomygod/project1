# SYSTEM SPECIFICATION REPORT

### PROJECT: ROLE-ISOLATED MEDICAL APPOINTMENT APPLICATION ARCHITECTURE

**DOCUMENT VERSION:** 3.0 (Production Release Blueprint)

\---

## 1\. UPDATED CORE PROJECT FOLDER TREE

The project structure has been refactored to separate the Patient (Public), Doctor (Private-Staff), and Administrator (Protected-Staff) views into isolated frontend and styling modules.

```text
hospital-booking-app/
│
├── backend/                        # Central Python Server Logic (FastAPI / Flask Engine)
│   ├── database/
│   │   ├── \_\_init\_\_.py
│   │   ├── connection.py           # Database transaction pipeline sessions manager
│   │   └── models.py               # SQL Row-to-Column structural schemas and relationship maps
│   │
│   ├── routes/
│   │   ├── auth.py                 # Handles token validation, password hashing, and user registration
│   │   ├── appointments.py         # Cascade routing fallback logic and calendar bookings
│   │   ├── reviews.py              # Background average star calculations and metric queries
│   │   ├── chat.py                 # Evaluates chatbot input strings and records log parameters
│   │   └── admin.py                # Admin core: invitation generation and token overrides
│   │
│   └── main.py                     # Primary core execution engine entry frame
│
├── frontend/                       # Presentation layer split to insulate individual UI logic
│   ├── css/                        # View-Specific Stylesheets
│   │   ├── patient/
│   │   │   ├── home.css            # Styles landing view, login boxes, and chatbot console frames
│   │   │   ├── profile.css         # Styling for demographic patient text inputs
│   │   │   ├── book.css            # Layout elements for multi-step sickness/date pick tables
│   │   │   ├── history.css         # Grid layouts for custom appointment timeline logs
│   │   │   ├── reviews.css         # Typography layouts for service score metric tables
│   │   │   └── about.css           # Styling for historical data parameters and cured counts
│   │   │
│   │   ├── doctor/
│   │   │   ├── invite-only.css     # Minimalist registration panel formatting
│   │   │   ├── login.css           # Private gateway portal styling
│   │   │   ├── requests.css        # Live incoming patient queue dashboard grids
│   │   │   ├── shift.css           # Hour-block spreadsheet calendar grid layouts
│   │   │   └── profile.css         # Style rules for qualification update fields
│   │   │
│   │   └── admin/                  # \[NEW SEPARATE FOLDER FOR ADMINISTRATORS]
│   │       ├── main.css            # Style rules for generating secret doctor invitation links
│   │       ├── stats.css           # Time-slotted daily matrix grid displaying system loads
│   │       └── staff.css           # 3-column card block layout system with action buttons
│   │
│   ├── js/
│   │   └── api.js                  # Asynchronous Network Call Controller (Frontend Interface Engine)
│   │
│   └── templates/                  # Role-Based Markup Layouts (Decoupled HTML Fragments)
│       ├── patient/
│       │   ├── home.html           # Public landing layout featuring login options and chat window
│       │   ├── profile.html        # Name, age, and gender demographic form data inputs
│       │   ├── book.html           # Multi-step medical slot reservation panel
│       │   ├── history.html        # Comprehensive patient history log
│       │   ├── reviews.html        # Aggregated community service and personnel reviews
│       │   └── about.html          # Public hospital profile overview (creation history, cured stats)
│       │
│       ├── doctor/
│       │   ├── invite-only.html    # Restricted token verification target account form
│       │   ├── login.html          # Gateway interface separating doctor authorization tracks
│       │   ├── requests.html       # Pending action logs dashboard enabling confirmations or cascades
│       │   ├── shift.html          # Timetable layout for assigned slots and medical history notes
│       │   └── profile.html        # Secure updating space for provider qualifications
│       │
│       └── admin/                  # \[NEW SEPARATE FOLDER FOR ADMINISTRATORS]
│           ├── main.html           # Master admin portal panel for generating secure token tokens
│           ├── stats.html          # High-density operational data view displaying all active slots
│           └── staff.html          # Hospital roster directory providing direct access termination
│
├── .env                            # Secure host credentials and private environment variable vault
├── .gitignore                      # Security rule configuration ignoring private system caches
└── requirements.txt                # System package dependency manifest log index
```

\---

## 2\. DETAILED FUNCTIONAL SPECIFICATION PER FILE

This directory catalog defines the exact functions operating inside every individual layout, ensuring you know precisely what logical code must be built for each interface page.

### A. Patient Public Web Domain

#### 1\. `patient/home.html` (`css/patient/home.css`)

* **`login\_with\_email()`**: Collects standard email text and password hashes from form boxes to post authorization validation payloads to the Python core.
* **`login\_with\_google()`**: Authenticates returning patient accounts via external Google identity provider configurations.
* **`send\_chat\_message()`**: Captures string tokens from the textbox element and passes arguments down into the Python live chatbot loop.
* **`stream\_bot\_response()`**: Appends clean, automated chat response blocks directly inside the browser display grid window.

#### 2\. `patient/profile.html` (`css/patient/profile.css`)

* **`save\_profile\_data()`**: Compiles validated patient attributes (legal full name, age, gender) to update persistent database identity structures.
* **`load\_existing\_profile()`**: Queries the server on page mount to automatically pre-fill user entry form blocks with stored profile metadata.

#### 3\. `patient/book.html` (`css/patient/book.css`)

* **`select\_patient\_target()`**: Controls systemic data arguments verifying if the booking entity is the primary profile user or a dependent relative.
* **`filter\_doctors\_by\_specialty()`**: Scans the targeted patient illness configuration parameters to fetch certified practitioners specialized in that clinical category.
* **`check\_available\_dates()`**: Disables blocked calendars or overlapping time intervals by parsing live physician shift assignment tables.

#### 4\. `patient/history.html` (`css/patient/history.css`)

* **`render\_calendar\_appointments()`**: Loops through all historically archived and pending client visit queries to structure a chronological calendar interface view.
* **`request\_appointment\_cancellation()`**: Submits an intentional update request to switch active slot configurations to a `canceled` status key state.

#### 5\. `patient/reviews.html` (`css/patient/reviews.css`)

* **`fetch\_overall\_service\_scores()`**: Compiles general clinic customer service tallies and facility operational ratings from database storage structures.
* **`fetch\_doctor\_star\_averages()`**: Displays read-only provider evaluation stars, drawing on fast server-calculated metric views.

#### 6\. `patient/about.html` (`css/patient/about.css`)

* **`fetch\_hospital\_metrics()`**: Requests live aggregated data logs containing historical statistics, such as the total volume of cured patients and the official establishment date milestones, to print on the public overview layout.

\---

### B. Restricted Medical Provider Portal Domain

#### 1\. `doctor/invite-only.html` (`css/doctor/invite-only.css`)

* **`verify\_invitation\_token()`**: Parses structural arguments right out of current browser URL queries to validate secure administrator access tokens.
* **`create\_doctor\_account()`**: Commits completed practitioner credentials, specializations, and password parameters directly into backend user rows.

#### 2\. `doctor/login.html` (`css/doctor/login.css`)

* **`authenticate\_doctor\_session()`**: Submits specific staff identification keys to acquire dynamic session token headers, steering them away from public user landing panels.

#### 3\. `doctor/requests.html` (`css/doctor/requests.css`)

* **`approve\_booking\_request()`**: Mutates target appointment states from a status of `pending` to `confirmed`, locking the time configuration for that physician.
* **`reject\_and\_trigger\_cascade()`**: Disclaims slot assignments and initiates automated background scripts to reroute the patient's illness parameter to the next alternative specialist available.

#### 4\. `doctor/shift.html` (`css/doctor/shift.css`)

* **`load\_daily\_shift\_hours()`**: Fills out local daily layout grids with active shift parameters, rest intervals, and assigned patient appointment hours.
* **`view\_patient\_medical\_history()`**: Unlocks safe access tunnels to examine historical clinical records and descriptions linked to the patient scheduled for the upcoming slot.

#### 5\. `doctor/profile.html` (`css/doctor/profile.css`)

* **`update\_medical\_qualifications()`**: Transmits professional licensing data adjustments, bio paragraphs, and updated profile photos directly to storage configurations.
* **`fetch\_personal\_review\_metrics()`**: Hydrates internal personal scorecards by rendering statistical feedback data sets specific to that clinician.

\---

### C. Protected Administrator Portal Workspace (New Subsystem)

#### 1\. `admin/main.html` (`css/admin/main.css`)

* **`generate\_secure\_invitation\_link()`**: Accepts targeted physician email entries to assemble random security tokens, saving the string parameters inside an `Invitations` schema to output a single-use onboarding URL path.
* **`fetch\_active\_invitation\_log()`**: Monitors previously distributed invitation links, listing chronological creation metrics alongside active expiration status flags.

#### 2\. `admin/stats.html` (`css/admin/stats.css`)

* **`load\_master\_day\_grid()`**: Builds a time-slotted institutional tracking grid mapping out every confirmed appointment occurrence across a 24-hour spreadsheet grid layout.
* **`apply\_live\_filter\_by\_doctor()`**: Dynamically updates the day matrix spreadsheet view to focus precisely on individual physician workload distributions or specific medical departments.

#### 3\. `admin/staff.html` (`css/admin/staff.css`)

* **`render\_staff\_card\_directory()`**: Generates a clean directory view displaying active hospital staff members inside structured 3-column rows (3 cards lined up horizontally per grid row).
* **`terminate\_staff\_access()`**: Instantly changes the `is\_active` parameter key of a chosen doctor's system identifier entry from `True` to `False`, forcing an immediate session block that logs them out and prevents subsequent entry attempts.

\---

### D. Asynchronous Frontend Interface Engine (`frontend/js/api.js`)

This global script forms the unified bridge connecting your front-end HTML elements to your Python endpoints.

* **`async handle\_http\_request(endpoint, method, payload)`**: The universal fetch engine that attaches security headers, routes parameters, and validates structural JSON outputs safely.
* **`async submit\_patient\_booking(booking\_details)`**: Bundles information from user forms and pushes structural booking fields directly to your scheduling routes.
* **`async transmit\_chat\_interaction(user\_message)`**: Passes user strings to the Python chatbot pipeline and streams returning automated text parameters back to the visual layout.
* **`async update\_doctor\_triage\_decision(appointment\_id, decision\_type)`**: Transmits clinician action parameters (approvals or cascade flags) directly to backend tracking logic.
* **`async execute\_admin\_action(target\_id, action\_payload)`**: Coordinates administrative commands, handling everything from generating token links to deactivating staff accounts.

\---

## 3\. BACKEND ROUTING INTERFACES (PYTHON SERVER HOOKS)

* **`backend/routes/auth.py`**:

  * `register\_public\_patient()` / `validate\_invitation\_token()` / `generate\_access\_token()`
* **`backend/routes/appointments.py`**:

  * `query\_available\_slots()` / `process\_cascade\_reroute()`
* **`backend/routes/reviews.py`**:

  * `commit\_new\_review()` / `recalculate\_doctor\_rating\_average()`
* **`backend/routes/chat.py`**:

  * `evaluate\_chat\_intent()` / `log\_chat\_history()`
* **`backend/routes/admin.py` (New python file addition)**:

  * `create\_system\_invitation()` / `toggle\_user\_active\_status()` / `query\_master\_schedule\_stream()`

