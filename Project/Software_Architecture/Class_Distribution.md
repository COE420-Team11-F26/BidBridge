# BidBridge — Class Distribution

**Course:** COE420L Software Engineering — Lab 8  
**Exercise:** 3 — Identify Components and Distribute Project Classes  
**Project:** BidBridge  

## Component-to-class distribution

Each approved Lab 5 class has **exactly one primary component**. A component may depend on classes in another component without taking ownership of them.

| ID | Component name | Layer | Responsibilities | Included classes | Count |
|---|---|---|---|---|---:|
| C01 | Presentation & Web Interface | Presentation | Displays pages, collects inputs and communicates with application services. | — (not modeled in Lab 5) | 0 |
| C02 | Account & Administration Management | Application | Manages accounts, role profiles, authentication, skills, portfolios and moderation. | `User`, `Client`, `Freelancer`, `Administrator`, `UserProfile`, `Skill`, `PortfolioItem`, `ModerationAction`, `AccountService` | 9 |
| C03 | Jobs & Bidding Management | Application | Manages jobs, searches, bids, notifications and bid history. | `Job`, `Bid`, `Notification`, `JobSearch`, `BidHistory` | 5 |
| C04 | Work Delivery & Dispute Management | Application | Manages work submissions, messages, revision requests, ratings and disputes. | `JobActivity`, `WorkSubmission`, `SubmissionFile`, `JobMessage`, `RevisionRequest`, `Rating`, `Dispute` | 7 |
| C05 | Escrow & Payment Management | Application | Manages escrow, simulated payments, transaction history and balances. | `Escrow`, `Transaction`, `PaymentService`, `SimulatedPaymentService`, `PlatformBalance` | 5 |
| C06 | Data Persistence & Storage | Data | Stores/retrieves records and provides backup/recovery support. | — (not modeled in Lab 5) | 0 |
| **Total** | **6 components** | | | **All 26 unique Lab 5 classes assigned once** | **26** |

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

**Shared classes in the original per-section tables:** `Job`, `User`, `Client`, `Freelancer`, and `Administrator` appear again in Section 3, but each has one primary assignment above. The Section 4 class IDs `C01`–`C05` are taken directly from the inventory and are distinct from the architectural component IDs.

## Assignment decisions and constraints

- `Client`, `Freelancer` and `Administrator` remain subclasses of `User` in **C02**. Other components reference these role classes when necessary without duplicating them.
- `Skill` stays with account/profile functionality in **C02** even though `Job` in **C03** references required skills. This is a cross-component relationship, not duplicate ownership.
- `Job` belongs to **C03**; C04 and C05 reference it for delivery, disputes and escrow rather than placing new copies of the class in those components.
- `Notification` is owned by **C03** because it was grouped with jobs and bidding in the Lab 5 inventory. Other components may request notifications through its interface later.
- `JobActivity` and its subclasses `WorkSubmission`, `JobMessage`, `RevisionRequest` and `Rating` are grouped in **C04**, preserving the Lab 5 inheritance structure.
- `PaymentService` (interface) and `SimulatedPaymentService` (implementation) remain together in **C05**.
- **C01 and C06 have no classes from the consolidated Lab 5 model**, because Lab 5 identified domain/application classes rather than UI controllers, database adapters, or repository classes. They are included to represent the selected three-layer architecture without inventing classes. If the team has since developed those classes, add them to the current UML and revise this distribution accordingly.

## Consistency check

- Number of architectural components: **6** (within the required 4–6).
- Number of original class inventory rows: **31** (including five repeat entries).
- Number of unique Lab 5 classes: **26**.
- Number of unique classes assigned: **26**.
- Classes assigned to multiple primary components: **0**.
- Unassigned approved classes: **0**.
- Cross-layer rule: **Presentation → Application → Data**; no Presentation → Data dependency.
