# BidBridge — Team Integration Notes

**Course:** COE420L Software Engineering — Lab 5  
**Part:** B — Team Integration, Exercise 3  
**Purpose:** Explain how the four individual class models were consolidated into one connected UML model.

## 1. Summary

The team model combines Accounts and Administration (P1/P7), Jobs and Bidding (P2/P3), Work Delivery and Disputes (P4/P6), and Escrow and Payments (P5). We kept **26 unique classes** from the individual inventories and reused shared classes instead of copying them into multiple sections. The consolidated Draw.io model connects the sections through users, jobs, activities, disputes, and escrow.

## 2. Duplicate classes resolved

| Duplicate or overlap | Integration decision | Reason |
|---|---|---|
| `User` in S1 and S3 | Use one `User` from Section 1 and connect it to notifications, activities, disputes, and ratings. | All users share the same identity and login state. |
| `Client` in S1 and S3; referenced in S2 | Use one `Client` subclass of `User`, with responsibilities for posting, reviewing, revising, and rating jobs. | Prevents role conflicts. |
| `Freelancer` in S1 and S3; referenced in S2/S4 | Use one `Freelancer` subclass of `User`, with skills, portfolio, bids, submissions, and platform balance. | Keeps the freelancer role consistent. |
| `Administrator` in S1 and S3 | Use one `Administrator` subclass of `User`, with moderation and dispute resolution behavior. | One administrator role supports both P7 and P6. |
| `Job` in S2 and S3; referenced in S4 | Use one `Job` from Section 2 and extend its lifecycle associations to activities, disputes, and escrow. | A job is the main shared business object. |

No artificial classes were added solely to increase the class count.

## 3. Inheritance and interface decisions

1. `Client`, `Freelancer`, and `Administrator` specialize `User` and inherit its shared account fields and methods.
2. `JobActivity` acts as a parent for `WorkSubmission`, `JobMessage`, `RevisionRequest`, and `Rating`. Each activity belongs to exactly one job and has exactly one author.
3. `PaymentService` is an interface. `SimulatedPaymentService` implements it so payment behavior can be replaced later without changing the job and escrow components.
4. `JobSearch` and `BidHistory` are query/service objects that read jobs or bids; they should not store separate permanent copies of those entities.

## 4. Connections between sections

| Cross-section connection | Purpose |
|---|---|
| `Client` → `Job` | A registered client posts jobs. |
| `Freelancer` → `Bid` → `Job` | A registered freelancer makes an offer for an open job. |
| `User` → `Notification` | Users receive updates about bidding and work. |
| `Job` → `JobActivity` → activity subclasses | Submissions, messages, revision requests, and ratings are recorded against jobs. |
| `Administrator` → `Dispute` → `Job` | The administrator handles a dispute about an assigned/submitted job. |
| `Job` → `Escrow` → `Transaction` | Accepted bids lead to a hold and eventual release or refund. |
| `Dispute` → `Escrow` | An open dispute freezes escrow until a resolution. |
| `Escrow` → `PaymentService` | The escrow uses the payment boundary to perform simulated transfers. |

## 5. Key multiplicity and constraint decisions

| Relationship or rule | Final integration decision |
|---|---|
| `Administrator` — `ModerationAction` | Each action has one administrator; an administrator performs `0..*` actions. |
| `ModerationAction` — `User` | Each action targets exactly one user; a user may be the target of `0..*` actions. |
| `User` — `UserProfile` | One-to-one. |
| `Client` — `Job` | Each job has one client; a client posts `0..*` jobs. |
| `Job` — `Bid` | Each bid belongs to one job; a job receives `0..*` bids. |
| `Freelancer` — `Bid` | Each bid belongs to one freelancer; a freelancer places `0..*` bids. |
| `Job` — accepted `Bid` | A job has `0..1` accepted bid, and an Assigned job must have one; the accepted bid must be among that job's bids. |
| `Job` — `JobActivity` | One job has `0..*` activities; every activity has one job. |
| `User` — `JobActivity` | One user authors `0..*` activities; every activity has one author. |
| `Job` — `Dispute` | One job can have `0..*` disputes; each dispute is for one job. |
| `Administrator` — `Dispute` | A dispute has `0..1` resolver until it is resolved; then exactly one. One administrator can resolve `0..*` disputes. |
| `WorkSubmission` — `SubmissionFile` | Each submission contains `1..5` files, maximum **25 MB per file**. |
| `WorkSubmission` — `RevisionRequest` | A submission may have `0..*` revision requests. |
| `Job` — `Escrow` | A job is secured by `0..1` escrow; an escrow belongs to one job. |
| `Escrow` — `Transaction` | Consolidated UML uses `0..*` transactions per escrow for a short newly created state. Section 4's individual diagram uses `1..*`; **team verification needed**. |
| `Escrow` — `PaymentService` | Each escrow uses one payment service; the service may be used by multiple escrows. |

## 6. Business rules carried into the shared model

- **Accounts:** Suspended accounts must not pass login validation. Every suspend, reactivate, hide, or remove moderation action requires a non-empty written reason.
- **Jobs and bids:** Jobs have a title, description, required skills, deadline and status. Bids may be edited or withdrawn only while the job is Open and before the deadline. A job may accept **at most one** bid.
- **Delivery:** Each work submission includes 1–5 files, each no larger than 25 MB; the client may approve work or request revisions.
- **Ratings:** Ratings are from 1 to 5 stars and are allowed after completion.
- **Disputes:** Disputes can be opened when a job is Assigned or Submitted. Administrators resolve disputes by choosing pay freelancer or refund client.
- **Payments:** Accepting a bid creates/holds escrow. An active dispute freezes escrow. Approval or a pay decision releases funds; a refund decision returns them. Every hold, release, or refund is recorded in transaction history.

## 7. Conflicts and follow-up checks

| Issue | Why it matters | Proposed resolution / owner action |
|---|---|---|
| Escrow–Transaction lower bound | S4 individual model says `1..*`; the consolidated diagram uses `0..*`. | If escrow and Hold transaction are created atomically, change final diagram to `1..*`; otherwise document the brief `0`-transaction state and require at least one Hold when Held. |
| Exact Section 1 use-case numbers | The Lab 5 inventory labels these use cases by name, not ID. | Cross-check with `Project/Requirements/Use_Cases.md`; add actual IDs only after checking. |
| Job status list | Open and Assigned are explicit; other states arise in delivery/dispute flows. | Match status names and transitions to original functional requirements and use cases. |
| Revision or cancellation rules | Individual sections mention revisions but not all lifecycle transitions. | Confirm allowed state changes with Labs 1–4 before implementing methods. |
| Attribute/method signatures | Individual diagrams may use different identifiers and return types. | Use one consistent `id` and timestamp convention and inspect the editable final UML for visibility/types. |

## 8. Final team deliverables

- `Class_Inventory.md` — approved class list and duplicate resolution.
- `Integration_Notes.md` — this consolidation record.
- `Class_Model_Consistency_Check.md` — traceability and multiplicity verification.
- `Class_Diagram/` — one consolidated editable UML diagram, not four disconnected diagrams.
- `Individual_Models/` — retain each student's individual diagram/table as evidence of contribution.


