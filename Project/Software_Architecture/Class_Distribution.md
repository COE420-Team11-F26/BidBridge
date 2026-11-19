# BidBridge — Class Distribution

**Course:** COE420L Software Engineering — Lab 8  
**Exercise:** 3 — Identify Components and Distribute Project Classes  
**Project:** BidBridge  

## Component-to-class distribution

Each class has **exactly one primary component**. This covers the 26 Lab 5 classes and the 6 classes added in Lab 8 for the Presentation and Data components. A component may depend on classes in another component without taking ownership of them.

| ID | Component name | Layer | Responsibilities | Included classes | Count |
|---|---|---|---|---|---:|
| C01 | Presentation & Web Interface | Presentation | Displays pages, collects inputs and communicates with application services. | `WebController`, `PageRenderer` (added in Lab 8) | 2 |
| C02 | Account & Administration Management | Application | Manages accounts, role profiles, authentication, skills, portfolios and moderation. | `User`, `Client`, `Freelancer`, `Administrator`, `UserProfile`, `Skill`, `PortfolioItem`, `ModerationAction`, `AccountService` | 9 |
| C03 | Jobs & Bidding Management | Application | Manages jobs, searches, bids, notifications and bid history. | `Job`, `Bid`, `Notification`, `JobSearch`, `BidHistory` | 5 |
| C04 | Work Delivery & Dispute Management | Application | Manages work submissions, messages, revision requests, ratings and disputes. | `JobActivity`, `WorkSubmission`, `SubmissionFile`, `JobMessage`, `RevisionRequest`, `Rating`, `Dispute` | 7 |
| C05 | Escrow & Payment Management | Application | Manages escrow, simulated payments, transaction history and balances. | `Escrow`, `Transaction`, `PaymentService`, `SimulatedPaymentService`, `PlatformBalance` | 5 |
| C06 | Data Persistence & Storage | Data | Stores/retrieves records and provides backup/recovery support. | `UserRepository`, `JobRepository`, `ActivityRepository`, `PaymentRepository` (added in Lab 8) | 4 |
| **Total** | **6 components** | | | **All 32 classes assigned once (26 from Lab 5 + 6 added in Lab 8)** | **32** |

## Assignment by class (verified against uploaded inventory)

This detailed list can be used when drawing each component and its assigned classes in Exercise 5.

| Lab 5 class ID | Lab 5 class | Primary component | Layer |
|---|---|---|---|
| `S1-C01` | `User` | C02 — Account & Administration Management | Application |
| `S1-C02` | `Client` | C02 — Account & Administration Management | Application |
| `S1-C03` | `Freelancer` | C02 — Account & Administration Management | Application |
| `S1-C04` | `Administrator` | C02 — Account & Administration Management | Application |
| `S1-C05` | `UserProfile` | C02 — Account & Administration Management | Application |
| `S1-C06` | `Skill` | C02 — Account & Administration Management | Application |
| `S1-C07` | `PortfolioItem` | C02 — Account & Administration Management | Application |
| `S1-C08` | `ModerationAction` | C02 — Account & Administration Management | Application |
| `S1-C09` | `AccountService` | C02 — Account & Administration Management | Application |
| `S2-C01` | `Job` | C03 — Jobs & Bidding Management | Application |
| `S2-C02` | `Bid` | C03 — Jobs & Bidding Management | Application |
| `S2-C03` | `Notification` | C03 — Jobs & Bidding Management | Application |
| `S2-C04` | `JobSearch` | C03 — Jobs & Bidding Management | Application |
| `S2-C05` | `BidHistory` | C03 — Jobs & Bidding Management | Application |
| `S3-C06` | `JobActivity` | C04 — Work Delivery & Dispute Management | Application |
| `S3-C07` | `WorkSubmission` | C04 — Work Delivery & Dispute Management | Application |
| `S3-C08` | `SubmissionFile` | C04 — Work Delivery & Dispute Management | Application |
| `S3-C09` | `JobMessage` | C04 — Work Delivery & Dispute Management | Application |
| `S3-C10` | `RevisionRequest` | C04 — Work Delivery & Dispute Management | Application |
| `S3-C11` | `Rating` | C04 — Work Delivery & Dispute Management | Application |
| `S3-C12` | `Dispute` | C04 — Work Delivery & Dispute Management | Application |
| `C01` | `Escrow` | C05 — Escrow & Payment Management | Application |
| `C02` | `Transaction` | C05 — Escrow & Payment Management | Application |
| `C03` | `PaymentService` | C05 — Escrow & Payment Management | Application |
| `C04` | `SimulatedPaymentService` | C05 — Escrow & Payment Management | Application |
| `C05` | `PlatformBalance` | C05 — Escrow & Payment Management | Application |
| `L8-C01` | `WebController` | C01 — Presentation & Web Interface | Presentation |
| `L8-C02` | `PageRenderer` | C01 — Presentation & Web Interface | Presentation |
| `L8-C03` | `UserRepository` | C06 — Data Persistence & Storage | Data |
| `L8-C04` | `JobRepository` | C06 — Data Persistence & Storage | Data |
| `L8-C05` | `ActivityRepository` | C06 — Data Persistence & Storage | Data |
| `L8-C06` | `PaymentRepository` | C06 — Data Persistence & Storage | Data |

**Shared classes in the original per-section tables:** `Job`, `User`, `Client`, `Freelancer`, and `Administrator` appear again in Section 3, but each has one primary assignment above. The Section 4 class IDs `C01`–`C05` are taken directly from the inventory and are distinct from the architectural component IDs.

## Assignment decisions and constraints

- `Client`, `Freelancer` and `Administrator` remain subclasses of `User` in **C02**. Other components reference these role classes when necessary without duplicating them.
- `Skill` stays with account/profile functionality in **C02** even though `Job` in **C03** references required skills. This is a cross-component relationship, not duplicate ownership.
- `Job` belongs to **C03**; C04 and C05 reference it for delivery, disputes and escrow rather than placing new copies of the class in those components.
- `Notification` is owned by **C03** because it was grouped with jobs and bidding in the Lab 5 inventory. Other components may request notifications through its interface later.
- `JobActivity` and its subclasses `WorkSubmission`, `JobMessage`, `RevisionRequest` and `Rating` are grouped in **C04**, preserving the Lab 5 inheritance structure.
- `PaymentService` (interface) and `SimulatedPaymentService` (implementation) remain together in **C05**.
- **C01 and C06 received new classes in Lab 8.** Lab 5 identified domain classes only, so `WebController` and `PageRenderer` (C01) and four repository classes (C06) were added to the team class diagram. Each repository stores the classes of one application component: `UserRepository` for C02, `JobRepository` for C03, `ActivityRepository` for C04 and `PaymentRepository` for C05.

## Consistency check

- Number of architectural components: **6** (within the required 4–6).
- Number of original class inventory rows: **31** (including five repeat entries).
- Number of unique Lab 5 classes: **26**.
- Classes added in Lab 8 (C01 and C06): **6**.
- Number of unique classes assigned: **32**.
- Classes assigned to multiple primary components: **0**.
- Unassigned approved classes: **0**.
- Cross-layer rule: **Presentation → Application → Data**; no Presentation → Data dependency.
