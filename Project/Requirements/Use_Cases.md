# BidBridge — Use Cases

## Individual Contributions

### Emran Lotfi

| UC ID | Use Case Name | Primary Actor | Short Description | Contributor |
| --- | --- | --- | --- | --- |
| UC-01 | Accept Bid and Fund Escrow | Client | Client selects one bid for an open job; the system holds the bid amount in escrow, assigns the freelancer, and notifies all bidders. | Emran Lotfi |
| UC-02 | Submit Work | Freelancer | Assigned freelancer uploads deliverable files and a note; the job moves to Submitted and the client is notified. | Emran Lotfi |
| UC-03 | Review Submission | Client | Client reviews the delivered files and either approves the work or requests a revision with a comment. | Emran Lotfi |
| UC-04 | Release Escrow Payment | Client (secondary: Freelancer) | The escrowed amount is transferred to the freelancer's balance, the transaction is recorded, and the job is marked Completed. | Emran Lotfi |
| UC-05 | Open Dispute | Client / Freelancer (secondary: Administrator) | Either party raises a dispute on an active job; escrow is frozen and the case is sent to an administrator for resolution. | Emran Lotfi |


### Marwan Ahmed

| UC ID | Use Case Name | Primary Actor | Short Description | Contributor |
| --- | --- | --- | --- | --- |
| UC-06 | Log In | Client / Freelancer / Administrator | A registered user enters their email address and password to access their account and the appropriate system features for their role. | Marwan Ahmed |
| UC-07 | View and Compare Bids | Client | The client opens one of their jobs, views the submitted bids, and compares freelancers based on price, delivery time, and rating. | Marwan Ahmed |
| UC-08 | Edit or Withdraw Bid | Freelancer | A freelancer changes the price or delivery time of an existing bid, or removes the bid, while the job is still open. | Marwan Ahmed |
| UC-09 | Send Job Message | Client / Freelancer | The client and the assigned freelancer exchange messages about the active job, such as questions, progress updates, or revision details. | Marwan Ahmed |
| UC-10 | Manage Profile and Portfolio | Client / Freelancer | A user updates their profile information. A freelancer may also update their skills, biography, and portfolio information. | Marwan Ahmed |


### Khalifa Alsuwaidi

| UC ID | Use Case Name | Primary Actor | Short Description | Contributor |
| --- | --- | --- | --- | --- |
| UC-11 | View Bid Notifications | Client | The client views notifications for newly submitted bids on their job postings. Each notification displays the related job, freelancer, bid price and submission time. | Khalifa Alsuwaidi |
| UC-12 | View submitted bid history | Freelancer | The freelancer views all bids they have previously submitted, including the related job, bid amount, proposed delivery time, and current bid status such as pending, accepted, rejected, or withdrawn. | Khalifa Alsuwaidi |
| UC-13 | Moderate User Account | Platform Administrator | The administrator reviews a user account and may suspend or reactivate the account when necessary. The administrator records a reason for the moderation action. | Khalifa Alsuwaidi |
| UC-14 | Moderate Job Posting | Platform Administrator | The administrator reviews reported or inappropriate job postings and may hide or remove a posting that violates platform rules while recording the reason for the action. | Khalifa Alsuwaidi |
| UC-15 | View Transaction History | Client, Freelancer | A client or freelancer views their payment transaction history, including the related job, transaction amount, payment status, transaction type, and timestamp. | Khalifa Alsuwaidi |


### Mohamed ElZefzafy

| UC ID | Use Case Name | Primary Actor | Short Description | Contributor |
| --- | --- | --- | --- | --- |
| UC-16 | Register a New account | Client and Freelancer | A new user signs up on the platform by entering their email and a password into their correct spots in the sign up page, and then by choosing their role either as a client or freelancer. | Mohamed ElZefzafy |
| UC-17 | Create task posting | Client | A Client creates a new task posting on the platform, specifying the task title, a detailed description, the required skills and a bidding deadline. | Mohamed ElZefzafy |
| UC-18 | Place initial bid | Freelancer | An eligible freelancer submits a new bid proposal for a specific task posting, specifying their bid, estimated completion time, and information about themselves or a CV. | Mohamed ElZefzafy |
| UC-19 | Search Open tasks | Freelancer | A freelancer can search and filter active task listings based off of the task title, or the required skills for that task . | Mohamed ElZefzafy |
| UC-20 | Submit Star Ratings | Client, Freelancer | Following the successful completion of a task and payment, the client and freelancer each submit a 1 to 5 star rating for each other. | Mohamed ElZefzafy |


## Use Case Relationships

| Relationship ID | Base Use Case | Related Use Case | Relationship | Justification |
| --- | --- | --- | --- | --- |
| R-01 | UC-03 Review Submission | UC-04 Release Escrow Payment | «extend» | Payment release happens only under a condition: the client approves the work. If a revision is requested, it does not run. |
| R-02 | UC-03 Review Submission | UC-05 Open Dispute | «extend» | Optional behavior: the client may dispute the submission instead of approving it or requesting a revision. |
| R-03 | Admin "Resolve Dispute" (team UC) | UC-04 Release Escrow Payment | «include» | Every dispute resolution must move the frozen escrow (to the freelancer or back to the client), so it always reuses the release/transfer behavior. |
| R-04 | UC-17 Create Task posting | UC-06 Log in | «include» | To create a task posting you have to be logged in with your client account. |
| R-05 | UC-18 Place initial Bid | UC-06 Log in | «include» | To place a bid for a task you have to be logged in with your freelancer account. |
| R-06 | UC-04 Release Escrow Payment | UC-20 submit Star rating | «extend» | Rating the other client / freelancer is an optional step that happens after release of the payment, meaning successful task completion. |
| R-07 | UC-07 View and Compare Bids | UC-01 Accept Bid and Fund Escrow | «extend» | While viewing and comparing submitted bids, the client may choose to accept one of them. Accepting a bid is optional because the client can compare bids without selecting one. |
| R-08 | UC-12 View Submitted Bid History | UC-08 Edit or Withdraw Bid | «extend» | While viewing their submitted bids, a freelancer may choose to edit or withdraw a bid if the job is still open and the bid has not been accepted. This action is optional and only applies to eligible bids. |
| R-09 | UC-03 Review Submission | UC-09 Send Job Message | «extend» | While reviewing submitted work, the client may send a message to the freelancer to ask a question or discuss changes. Messaging is optional and is not required every time a submission is reviewed. |
| R-10 | UC-11 View Bid Notifications | UC-07 View and Compare Bids | «extend» | After viewing a bid notification, the client may choose to open the related job and compare all submitted bids. This action is optional because the client can simply view the notification without comparing bids. |
| R-11 | UC-14 Moderate Job Posting | UC-13 Moderate User Account | «extend» | While reviewing a job posting that violates platform rules, the administrator may also decide to suspend the responsible user's account. This is optional because removing or hiding a posting does not always require suspending its owner. |
| R-11 | UC-05 Open Dispute | UC-15 View Transaction History | «extend» | While opening a dispute, the client or freelancer may choose to review the related payment transaction history to verify the escrow or payment status. This step is optional because a dispute can be submitted without reviewing transaction history. |