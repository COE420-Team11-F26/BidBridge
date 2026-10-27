# BidBridge — Class Model Consistency and Traceability Check

**Course:** COE420L Software Engineering — Lab 5  
**Part:** B — Team Integration, Exercise 3  
**Purpose:** Check that the consolidated class model represents the functionality and associations described by the individual models.


## 1. Process and use-case traceability

| Process | Required functionality | Classes representing it | Lab 5 use cases / reference | Consistency observation |
|---|---|---|---|---|
| P1 — Accounts | Register, log in/out, manage profile, skills and portfolio; block suspended users | `User`, `Client`, `Freelancer`, `UserProfile`, `Skill`, `PortfolioItem`, `AccountService` | Section 1: Registration, Login, Account Status, Manage Profile, Manage Skills, Portfolio | Covered through shared users and account-related objects. |
| P7 — Administration | Suspend, reactivate, hide and remove, each with a written reason | `Administrator`, `ModerationAction`, `User`, `UserProfile` | Section 1: Moderate Accounts / Content | Action, administrator, target and reason represented. |
| P2 — Jobs | Post job with title, description, required skills, deadline and status; keyword search | `Client`, `Job`, `Skill`, `JobSearch` | Section 2: UC-01, UC-07, UC-17, UC-19 | Job's posting client and searchable required skills represented. |
| P3 — Bidding / notifications | Place, edit/withdraw, list/sort bids, preserve bid history, accept at most one; send notices | `Job`, `Bid`, `Freelancer`, `BidHistory`, `Notification`, `User` | Section 2: UC-01, UC-07, UC-08, UC-12, UC-18, UC-02, UC-11 | Bid/job/freelancer associations and accepted-bid constraint represented. |
| P4 — Work delivery / communication | Submit 1–5 files (≤25 MB each), communicate, approve or request revisions, rate 1–5 | `Job`, `JobActivity`, `WorkSubmission`, `SubmissionFile`, `JobMessage`, `RevisionRequest`, `Rating`, `User`, `Client`, `Freelancer` | Section 3: UC-02, UC-03, UC-09, UC-20 | Activity inheritance and file count/size constraints represented. |
| P6 — Disputes | Open on Assigned/Submitted jobs and have admin decide pay/refund | `Dispute`, `Job`, `Administrator`, `User`, `Escrow` | Section 3: UC-05, Admin Resolve Dispute | Dispute belongs to job, optional pending resolver, and escrow freeze link represented. |
| P5 — Escrow payments | Hold on acceptance; freeze on dispute; release/refund; transaction history; simulated service | `Job`, `Escrow`, `Transaction`, `PaymentService`, `SimulatedPaymentService`, `PlatformBalance`, `Freelancer` | Section 4: FR-01, FR-04, FR-05, FR-20; NFR-02, NFR-05; UC-01, UC-04, UC-05, UC-15; D5 Transactions | Escrow/service/transaction and balance responsibilities represented. |

## 2. Association and multiplicity checks

| Relationship | Expected multiplicity or UML relationship | Check |
|---|---|---|
| `Client`, `Freelancer`, `Administrator` → `User` | Generalization (inheritance) | Meets common-user model. |
| `User` — `UserProfile` | `1` ↔ `1` | Each user has one profile. |
| `Freelancer` — `Skill` | `0..*` ↔ `0..*` | Freelancer can have many skills; skills can be shared. |
| `Freelancer` — `PortfolioItem` | Each portfolio item has `1` freelancer; a freelancer has `0..*` items | Portfolio ownership modeled. |
| `Administrator` — `ModerationAction` | Each action has `1` administrator; admin performs `0..*` actions | Audit attribution modeled. |
| `ModerationAction` — `User` | Each action targets `1` user; user has `0..*` actions | Target accountability modeled. |
| `Client` — `Job` | Each job posted by `1` client; client has `0..*` jobs | Posting modeled. |
| `Job` — `Bid` | Each bid belongs to `1` job; job has `0..*` bids | Bid ownership modeled. |
| `Freelancer` — `Bid` | Each bid belongs to `1` freelancer; freelancer has `0..*` bids | Bid author modeled. |
| `Job` — accepted `Bid` | `0..1` accepted bid per job | At most one; if Assigned, exactly one. |
| `User` — `Notification` | Each notification goes to `1` user; user receives `0..*` notifications | Recipient modeled. |
| `Job` — `Skill` | Job requires `0..*` skills (team model) | Searchable skills represented; confirm minimum if requirement requires at least one. |
| `Job` — `JobActivity` | Each activity belongs to `1` job; job has `0..*` activities | Recorded work lifecycle. |
| `User` — `JobActivity` | Each activity has `1` author; user authors `0..*` activities | Audit author modeled. |
| `WorkSubmission`, `JobMessage`, `RevisionRequest`, `Rating` → `JobActivity` | Generalization | No duplicated job/author references needed in each subtype. |
| `WorkSubmission` — `SubmissionFile` | Each submission has `1..5` files | File count validated. |
| `WorkSubmission` — `RevisionRequest` | Each submission has `0..*` revision requests | Multiple revision rounds possible. |
| `Job` — `Dispute` | Each dispute belongs to `1` job; job may have `0..*` disputes | Dispute context modeled. |
| `User` — `Dispute` | Each dispute opened by `1` user; user may open `0..*` | Opening party modeled; must be client or assigned freelancer. |
| `Administrator` — `Dispute` | `0..1` admin per pending dispute, exactly `1` if resolved; admin resolves `0..*` | Pending/resolved distinction retained. |
| `User` — `Rating` | Each rating has one recipient; user may receive `0..*` ratings | Rating recipient modeled. |
| `Job` — `Escrow` | Each job has `0..1` escrow; escrow belongs to `1` job | Escrow created after acceptance. |
| `Escrow` — `Transaction` | Consolidated: `0..*` transactions per escrow; individual Section 4: `1..*` | **Pending team confirmation** (see §5). |
| `Dispute` — `Escrow` | Each dispute freezes its job's escrow, when present; an escrow can be involved in disputes over time | Payment freeze modeled. |
| `Freelancer` — `PlatformBalance` | One-to-one in Section 4 model | Earnings balance modeled. |
| `Transaction` — `PlatformBalance` | Release may credit one balance; Hold/Refund need not credit one | Transfer destination distinction modeled. |
| `Escrow` — `PaymentService` | Each escrow uses `1` service; service serves `0..*` escrows | Payment boundary modeled. |
| `SimulatedPaymentService` → `PaymentService` | Interface realization | Simulated implementation modeled. |
| `JobSearch` → `Job`; `BidHistory` → `Bid`; `AccountService` → `User` | Dependencies rather than ownership | Does not duplicate stored records. |

## 3. Functional invariant checks

| Invariant | Expected system behavior | UML class responsible | Status |
|---|---|---|---|
| Account eligibility | Suspended/removed accounts cannot log in | `User`, `AccountService` | Modeled; enforce in authentication logic. |
| Moderation reason | Each moderation action has a non-empty written reason | `ModerationAction` | Modeled; enforce as required validation. |
| Bid editing | Edit/withdraw only when job is Open and before bid deadline | `Job`, `Bid` | Modeled as rule; requires method guard. |
| Accepted bid | At most one accepted bid; assigned job has one | `Job`, `Bid` | Modeled; accepted bid must belong to same job. |
| Submission attachments | Between one and five files per submission | `WorkSubmission`, `SubmissionFile` | Modeled in multiplicity. |
| Submission file size | Each file no larger than 25 MB | `SubmissionFile`, submission validation | Modeled as constraint. |
| Ratings | Star value is an integer from 1 to 5, after completion | `Rating`, `Job` | Modeled as constraint. |
| Dispute eligibility | Only client or assigned freelancer opens a dispute on Assigned/Submitted job | `Dispute`, `User`, `Job` | Modeled as rule; validate roles/states. |
| Escrow freeze | Open dispute freezes held funds; frozen funds are not releasable | `Dispute`, `Escrow` | Modeled; enforce in state transitions. |
| Escrow decision | Admin resolution pays freelancer OR refunds client, not both | `Administrator`, `Dispute`, `Escrow` | Modeled as mutually exclusive decision. |
| Transaction history | Hold/release/refund money movement creates a permanent transaction | `Escrow`, `Transaction` | Modeled; persistence required. |
| Simulated payment | Escrow uses `PaymentService` interface and the prototype implementation | `PaymentService`, `SimulatedPaymentService` | Modeled through interface realization. |

## 4. DFD and data-store checks

- **P1/P7:** The account and moderation objects represent user registration, authentication, profile management, and administrator actions.
- **P2/P3:** `Job`, `Bid`, and `Notification` represent posting, offers, and user updates. `JobSearch` and `BidHistory` read those records.
- **P4/P6:** `JobActivity` and `Dispute` represent work exchanges and dispute escalation, with `Job` connecting them to the correct assignment.
- **P5 / D5 Transactions:** `Transaction` stores hold, release, and refund history. `PaymentService` is the interface to the simulated payment system.



