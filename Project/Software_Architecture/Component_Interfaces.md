# BidBridge — Component Interfaces

**Course:** COE420L Software Engineering — Lab 8  
**Exercise:** 4 — Design Component Interfaces Using UML  
**Project:** BidBridge

Every operation below is taken from a class assigned to the component that provides the interface (team class diagram from Lab 5, updated in Lab 8 to match the Lab 6 sequence diagrams). The interfaces are drawn in the UML Component Diagram (Exercise 5) as lollipops (provided) and sockets (required).

## New classes added in Lab 8

The Presentation (C01) and Data (C06) components had no Lab 5 classes. These classes were added so their responsibilities and interfaces come from real class operations:

| Component | Class | Operations | Reason |
|---|---|---|---|
| C01 | `WebController` | `handleRequest(req: HttpRequest): HttpResponse` | Receives browser requests and calls the application interfaces. |
| C01 | `PageRenderer` | `render(page: String, data: Map): String` | Builds the pages shown to clients, freelancers and administrators. |
| C06 | `UserRepository` | `findById(id: int): User`, `save(u: User): void` | Stores accounts and profiles (D1 Users). |
| C06 | `JobRepository` | `findById(id: int): Job`, `findOpen(keyword: String): List`, `save(j: Job): void`, `saveBid(b: Bid): void` | Stores jobs and bids (D2 Jobs, D3 Bids). |
| C06 | `ActivityRepository` | `save(a: JobActivity): void`, `saveDispute(d: Dispute): void`, `findByJob(jobId: int): List` | Stores submissions, messages, ratings and disputes (D4, D6). |
| C06 | `PaymentRepository` | `saveEscrow(e: Escrow): void`, `saveTransaction(t: Transaction): void`, `findTransactions(userId: int): List` | Stores escrow and transaction records (D5 Transactions). |

## Interfaces

| Interface | Provided by | Required by | Operations | Source class |
|---|---|---|---|---|
| `IWeb` | C01 | Web Browser (external) | `handleRequest(req: HttpRequest): HttpResponse` | `WebController` |
| `IAccount` | C02 | C01 | `register(email: String, password: String, role: String): User`<br>`login(email: String, password: String): User`<br>`logout(user: User): void` | `AccountService` |
| `IProfile` | C02 | C01 | `updateDetails(name: String, bio: String): void`<br>`addSkill(s: Skill): void`<br>`addPortfolioItem(p: PortfolioItem): void` | `UserProfile`, `Freelancer` |
| `IModeration` | C02 | C01 | `moderate(u: User, t: ModerationType, reason: String): ModerationAction`<br>`suspendUser(u: User, reason: String): ModerationAction`<br>`reactivateUser(u: User, reason: String): ModerationAction` | `Administrator` |
| `IJobManagement` | C03 | C01, C02, C04 | `acceptsBids(now: DateTime): boolean`<br>`acceptBid(bid: Bid): boolean`<br>`changeStatus(status: JobStatus): void` | `Job` |
| `IBidding` | C03 | C01 | `placeBid(amount: Decimal, days: int, info: String): boolean`<br>`isEditable(): boolean`<br>`editBid(amount: Decimal, days: int): boolean`<br>`withdraw(): boolean`<br>`forFreelancer(f: Freelancer): List` | `Job`, `Bid`, `BidHistory` |
| `IJobSearch` | C03 | C01 | `search(keyword: String): List`<br>`sortBy(criteria: String): List` | `JobSearch` |
| `INotification` | C03 | C01 | `markRead(): void` | `Notification` |
| `IWorkDelivery` | C04 | C01 | `addFile(f: SubmissionFile): boolean`<br>`submit(): void`<br>`requestChanges(comment: String): void`<br>`send(): void` | `WorkSubmission`, `RevisionRequest`, `JobMessage` |
| `IDispute` | C04 | C01 | `open(reason: String): void`<br>`resolve(decision: ResolutionType): void` | `Dispute` |
| `IEscrow` | C05 | C03, C04 | `hold(): boolean`<br>`freeze(): void`<br>`release(): boolean`<br>`refund(): boolean` | `Escrow` |
| `ITransactionHistory` | C05 | C01 | `getDetails(): String`<br>`getBalance(): Decimal` | `Transaction`, `PlatformBalance` |
| `PaymentService` | `SimulatedPaymentService` (C05, prototype); external Payment / Escrow Service (production) | C05 (`Escrow`) | `holdFunds(payer: User, amount: Decimal): boolean`<br>`transfer(payee: User, amount: Decimal): boolean`<br>`refund(payer: User, amount: Decimal): boolean` | `PaymentService`, `SimulatedPaymentService` |
| `IUserData` | C06 | C02 | `findById(id: int): User`<br>`save(u: User): void` | `UserRepository` |
| `IJobData` | C06 | C03 | `findById(id: int): Job`<br>`findOpen(keyword: String): List`<br>`save(j: Job): void`<br>`saveBid(b: Bid): void` | `JobRepository` |
| `IActivityData` | C06 | C04 | `save(a: JobActivity): void`<br>`saveDispute(d: Dispute): void`<br>`findByJob(jobId: int): List` | `ActivityRepository` |
| `IPaymentData` | C06 | C05 | `saveEscrow(e: Escrow): void`<br>`saveTransaction(t: Transaction): void`<br>`findTransactions(userId: int): List` | `PaymentRepository` |

## Why the required interfaces are needed

- **Web Browser → `IWeb`:** Clients, freelancers and administrators use BidBridge through their browser, which sends every request to `WebController` in C01.
- **C01 → C02–C05:** The Presentation layer only talks to the Application layer (closed 3-layer style); it never uses a C06 interface.
- **C03 → `IEscrow`:** Accepting a bid holds the escrow before the job becomes Assigned (UC-01 sequence diagram, FR-01).
- **C04 → `IEscrow`, `IJobManagement`:** Approving work releases escrow and completes the job; opening a dispute freezes escrow; the admin's decision releases or refunds it (FR-04, FR-05).
- **C02 → `IJobManagement`:** An administrator can hide or remove a job posting (FR-19, UC-13).
- **C02–C05 → C06:** Each Application component stores its records through its own data interface, so the Application layer is the only one that reaches the Data layer.
- **C05 → `PaymentService`:** All money movement goes through one interface (NFR-05). `SimulatedPaymentService` realizes it in the prototype; a real external payment service can replace it later.
