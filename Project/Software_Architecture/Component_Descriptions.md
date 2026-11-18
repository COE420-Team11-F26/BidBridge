# BidBridge — Component Descriptions

**Course:** COE420L Software Engineering — Lab 8  
**Exercise:** 3 — Identify Components and Distribute Project Classes  
**Project:** BidBridge

## Architectural approach

BidBridge uses the **three-layer (closed) architecture** selected in Exercise 2:

1. **Presentation layer:** Presents the website to clients, freelancers and administrators.
2. **Application / Middleware layer:** Enforces business rules and coordinates the system's functions.
3. **Data layer:** Persists and retrieves application records.

Six architectural components are defined below. The four application-layer components follow the functional groupings in the consolidated Lab 5 class inventory. The Presentation and Data components are architectural boundaries, but the supplied Lab 5 class inventory does **not** define dedicated UI or repository/database classes. Their class lists are therefore empty rather than introducing classes that were not approved in Lab 5.

## Components

### C01 — Presentation & Web Interface

- **Layer:** Presentation
- **Responsibilities:** Presents BidBridge pages and forms, collects user input, displays search results, bids, submissions, notifications, and payment or dispute statuses. Sends requests to application services rather than accessing stored data directly.
- **Supported functionality:** Register and log in; view and edit a profile; browse jobs and bids; submit work; review disputes and payment status.
- **Assigned Lab 5 classes:** None modeled in Lab 5 (architectural component only).

### C02 — Account & Administration Management

- **Layer:** Application
- **Responsibilities:** Manages user identities, roles, authentication, account eligibility, freelancer profiles and skills, portfolios, and administrator moderation. Ensures suspended or removed accounts cannot authenticate and records a written reason for each moderation action.
- **Supported functionality:** Registration, login/logout, profile updates, managing skills and portfolios, suspending/reactivating accounts, hiding/removing content.
- **Assigned Lab 5 classes:** `User`, `Client`, `Freelancer`, `Administrator`, `UserProfile`, `Skill`, `PortfolioItem`, `ModerationAction`, `AccountService`

### C03 — Jobs & Bidding Management

- **Layer:** Application
- **Responsibilities:** Manages posting and searching jobs, bid placement and editing/withdrawal, job selection, bid history, and job-related notifications. Enforces bid deadlines and the rule that a job can have at most one accepted bid.
- **Supported functionality:** Post/search jobs; place, edit, withdraw, list, and accept bids; inspect bid history; notify participants about relevant job and bid events.
- **Assigned Lab 5 classes:** `Job`, `Bid`, `Notification`, `JobSearch`, `BidHistory`

### C04 — Work Delivery & Dispute Management

- **Layer:** Application
- **Responsibilities:** Manages the work lifecycle once a bid is accepted: submissions and attachments, client–freelancer messages, revision requests, post-completion ratings, and disputes requiring administrative resolution. Coordinates with payments when approval or dispute resolution changes escrow status.
- **Supported functionality:** Submit deliverables (1–5 files, each no larger than 25 MB); exchange job messages; request revisions; rate completed jobs; open and resolve disputes.
- **Assigned Lab 5 classes:** `JobActivity`, `WorkSubmission`, `SubmissionFile`, `JobMessage`, `RevisionRequest`, `Rating`, `Dispute`

### C05 — Escrow & Payment Management

- **Layer:** Application
- **Responsibilities:** Handles the financial workflow tied to accepted bids. Places funds in escrow, freezes them when a dispute is active, and releases or refunds them following the permitted job or dispute outcome. Records payment transactions and maintains the freelancer platform balance.
- **Supported functionality:** Hold, freeze, release, and refund escrow; simulate payment operations through the PaymentService interface; maintain transaction history.
- **Assigned Lab 5 classes:** `Escrow`, `Transaction`, `PaymentService`, `SimulatedPaymentService`, `PlatformBalance`

### C06 — Data Persistence & Storage

- **Layer:** Data
- **Responsibilities:** Stores and retrieves the persistent data used by the application components, including accounts, profiles, jobs, bids, submissions, disputes, escrow and transactions. Provides controlled data access and supports backup/recovery; application rules remain in the Application layer.
- **Supported functionality:** Store and retrieve system records; preserve transaction history; support backups and recovery.
- **Assigned Lab 5 classes:** None modeled in Lab 5 (architectural component only).

## Component interaction and layer rules

- **C01** sends requests to the relevant application services (**C02–C05**) and displays their results. It must not access **C06** directly.
- **C02** manages authorization and account restrictions used by other application components.
- **C03** coordinates with **C05** after bid acceptance so escrow is held before a payment-dependent job transition is finalized.
- **C04** coordinates with **C05** to freeze funds during disputes and to release or refund funds after the approved outcome.
- **C02–C05** access stored records through **C06**, not through direct requests from C01.
- Cross-component collaboration within the application layer does not bypass the three-layer boundary: **Presentation → Application → Data**.

## How the architecture supports the Exercise 1 design goals

| Design goal | Architectural support |
|---|---|
| G01 — Security | Authentication and moderation are centralized in C02; C01 cannot access storage directly. |
| G02 — Reliability | The job, dispute and payment flows coordinate in the application layer so payment and job status remain consistent. |
| G03 — Availability | C06 separates persistence and recovery responsibilities from the UI and business logic. |
| G04 — Performance | Job search/query functions in C03 and data access in C06 can be optimized independently of the UI. |

**Class inventory verification:** The supplied `Class_Inventory(1).md` contains 31 class rows across Sections 1–4, including repeat references to `Job`, `User`, `Client`, `Freelancer`, and `Administrator` in Section 3. After consolidating these shared classes, the document contains **26 unique classes**, all assigned once in `Class_Distribution.md`. The Section 4 class IDs (`C01`–`C05`) refer to class IDs, not the architectural component IDs.

