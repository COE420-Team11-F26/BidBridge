# Section 1: Accounts and Administration (Khalifa Alsuwaidi)

| Class ID | Class Name | Purpose / Responsibility | Related Use Case(s) | Contributor |
| :--- | :--- | :--- | :--- | :--- |
| S1-C01 | User | Shared account identity, credentials and account status; checks whether login is allowed. | Registration; Login; Account Status | Khalifa Alsuwaidi |
| S1-C02 | Client | Specialized User role for clients; shared with the Job and Bidding section. | Registration; Manage Profile | Khalifa Alsuwaidi |
| S1-C03 | Freelancer | Specialized User role that manages skills and portfolio items. | Registration; Manage Skills; Portfolio | Khalifa Alsuwaidi |
| S1-C04 | Administrator | Specialized User role that performs and records suspend, reactivate, hide and remove actions. | Moderate Accounts / Content | Khalifa Alsuwaidi |
| S1-C05 | UserProfile | Stores public profile details and whether the profile is visible. | View / Update Profile | Khalifa Alsuwaidi |
| S1-C06 | Skill | Represents a reusable skill associated with one or more freelancers. | Manage Freelancer Skills | Khalifa Alsuwaidi |
| S1-C07 | PortfolioItem | Stores a freelancer work sample, its description, link and visibility. | Manage Portfolio | Khalifa Alsuwaidi |
| S1-C08 | ModerationAction | Records the administrator, targeted user, action type, mandatory written reason and date. | Suspend; Reactivate; Hide; Remove | Khalifa Alsuwaidi |
| S1-C09 | AccountService | Handles account registration, authentication and logout; checks account status at login. | Registration; Login; Logout | Khalifa Alsuwaidi |

---

# Section 2: Jobs, Bidding, & Notifications (Mohamed ElZefzafy)

| Class ID | Class Name | Purpose/Responsibility | Related Use Case(s) | Contributor |
| :--- | :--- | :--- | :--- | :--- |
| S2-C01 | Job | Stores a posted job, including its title, description, skills, bid deadline and status. Checks if it still accepts bids and records the accepted bids. | UC-01, UC-07, UC-17, UC-19 | Mohamed ElZefzafy |
| S2-C02 | Bid | Stores a freelancers offer on a job, including the price, delivery time, and status. Can only be edited or withdrawn while the job is open. | UC-01, UC-07, UC-08, UC-12, UC-18 | Mohamed ElZefzafy |
| S2-C03 | Notification | Stores a message sent to a user such as a new bid or submitted work, and its time. | UC-02, UC-11 | Mohamed ElZefzafy |
| S2-C04 | JobSearch | Searches open jobs by keyword, matching the title and required skills. | UC-19 | Mohamed ElZefzafy |
| S2-C05 | BidHistory | Lists a freelancers submitted bids with job, amount, delivery time and status. | UC-12 | Mohamed ElZefzafy |

---

# Section 3: Job Activity, Submissions, & Disputes (Marwan Ahmed)

| Class ID | Class Name | Purpose/Responsibility | Related Use Case(s) | Contributor |
| :--- | :--- | :--- | :--- | :--- |
| S3-C01 | Job | Stores job information and tracks its status during submission, revision, completion, and disputes. | UC-02, UC-03, UC-05 | Marwan Ahmed |
| S3-C02 | User | Represents users who create job activities or open disputes. | UC-02, UC-05, UC-09, UC-20 | Marwan Ahmed |
| S3-C03 | Client | Reviews submitted work, requests revisions, sends messages, and gives ratings. | UC-03, UC-05, UC-09, UC-20 | Marwan Ahmed |
| S3-C04 | Freelancer | Submits completed work, communicates with clients, and gives ratings. | UC-02, UC-05, UC-09, UC-20 | Marwan Ahmed |
| S3-C05 | Administrator | Reviews disputes and decides whether to pay the freelancer or refund the client. | UC-05, Admin Resolve Dispute | Marwan Ahmed |
| S3-C06 | JobActivity | Represents activities recorded for a job, such as submissions, messages, revisions, and ratings. | UC-02, UC-03, UC-09, UC-20 | Marwan Ahmed |
| S3-C07 | WorkSubmission | Stores the freelancer's submitted work and submission note. | UC-02, UC-03 | Marwan Ahmed |
| S3-C08 | SubmissionFile | Stores information about an uploaded work file, including its name, size, and location. | UC-02 | Marwan Ahmed |
| S3-C09 | JobMessage | Stores messages exchanged between the client and assigned freelancer. | UC-09 | Marwan Ahmed |
| S3-C10 | RevisionRequest | Records a client's requested changes and written comment. | UC-03 | Marwan Ahmed |
| S3-C11 | Rating | Stores a 1–5 star rating given by a client or freelancer after job completion. | UC-20 | Marwan Ahmed |
| S3-C12 | Dispute | Stores the dispute reason, status, and administrator's resolution decision. | UC-05 | Marwan Ahmed |

---

# Section 4: Handle Escrow Payments (Emran Lotfi)

My part of the system is Level-0 DFD process P5 (Handle Escrow Payments): holding the escrow when a bid is accepted, releasing it on approval, refunding it, freezing it during a dispute, recording transactions, and the simulated payment service. The classes below come from FR-01, FR-04, FR-05 and FR-20, NFR-02 and NFR-05, use cases UC-01, UC-04, UC-05 and UC-15, scenarios S-03 to S-05, and data store D5 Transactions.

| Class ID | Class Name | Purpose / Responsibility | Related Use Case(s) | Contributor |
| :--- | :--- | :--- | :--- | :--- |
| C01 | Escrow | Holds the accepted bid amount for one job from bid acceptance until the work is approved or a dispute is settled. Its status moves Held → Frozen → Released / Refunded, and it cannot be released while Frozen (FR-01, FR-04, FR-05; NFR-02). | UC-01, UC-04, UC-05 | Emran Lotfi |
| C02 | Transaction | Permanent record of every money movement (hold, release, refund) with job ID, amount, payer, payee, type, status and timestamp. It is the source of each user's transaction history and matches data store D5 Transactions (FR-04, FR-20). | UC-04, UC-05, UC-15 | Emran Lotfi |
| C03 | PaymentService «interface» | The single boundary through which all money moves (hold, transfer, refund). It represents the Payment / Escrow Service entity in the DFD and lets the simulated escrow be replaced by a real provider without changing the job or bid modules (NFR-05). | UC-01, UC-04, UC-05 | Emran Lotfi |
| C04 | SimulatedPaymentService | The prototype implementation of PaymentService, required because the project scope uses a simulated escrow rather than real banking integration. It keeps simulated funds per user. | UC-01, UC-04, UC-05 | Emran Lotfi |
| C05 | PlatformBalance | A freelancer's platform balance, credited when an escrow is released (FR-04). It is kept in the payment section instead of inside Freelancer so payment data stays isolated (NFR-05). | UC-04, UC-15 | Emran Lotfi |
