# BidBridge — Section 3: Work Delivery, Communication and Disputes (P4, P6)

**Contributor:** Marwan Ahmed

## Exercise 1: Individual Class Inventory

| Class ID | Class Name | Purpose/Responsibility | Related Use Case(s) | Contributor |
|---|---|---|---|---|
| S3-C01 | Job | Stores job information and tracks its status during submission, revision, completion, and disputes. | UC-02, UC-03, UC-05 | Marwan Ahmed |
| S3-C02 | User | Represents users who create job activities or open disputes. | UC-02, UC-05, UC-09, UC-20 | Marwan Ahmed |
| S3-C03 | Client | Reviews submitted work, requests revisions, sends messages, and gives ratings. | UC-03, UC-05, UC-09, UC-20 | Marwan Ahmed |
| S3-C04 | Freelancer | Submits completed work, communicates with clients, and gives ratings. | UC-02, UC-05, UC-09, UC-20 | Marwan Ahmed |
| S3-C05 | Administrator | Reviews disputes and decides whether to pay the freelancer or refund the client. | UC-05, Admin Resolve Dispute (team UC) | Marwan Ahmed |
| S3-C06 | JobActivity | Represents activities recorded for a job, such as submissions, messages, revisions, and ratings. | UC-02, UC-03, UC-09, UC-20 | Marwan Ahmed |
| S3-C07 | WorkSubmission | Stores the freelancer's submitted work and submission note. | UC-02, UC-03 | Marwan Ahmed |
| S3-C08 | SubmissionFile | Stores information about an uploaded work file, including its name, size, and location. | UC-02 | Marwan Ahmed |
| S3-C09 | JobMessage | Stores messages exchanged between the client and assigned freelancer. | UC-09 | Marwan Ahmed |
| S3-C10 | RevisionRequest | Records a client's requested changes and written comment. | UC-03 | Marwan Ahmed |
| S3-C11 | Rating | Stores a 1–5 star rating given by a client or freelancer after job completion. | UC-20 | Marwan Ahmed |
| S3-C12 | Dispute | Stores the dispute reason, status, and administrator's resolution decision. | UC-05 | Marwan Ahmed |

## Class Selection Justification

These classes represent the main objects needed for P4 (Manage Work Delivery) and P6 (Resolve Disputes) in BidBridge. `JobActivity` is an abstract parent class for work submissions, messages, revision requests, and ratings because they are all activities associated with a job. `Dispute` is modeled separately because it has its own dispute status, assigned administrator, and pay-or-refund resolution process. `SubmissionFile` represents the individual files included with a work submission. `Job`, `User`, `Client`, `Freelancer`, and `Administrator` are shared system classes that should be consolidated with equivalent classes contributed by other teammates, rather than duplicated in the final team model.

## Exercise 2: UML Associations and Multiplicities

| Association | Multiplicity | Explanation |
|---|---|---|
| Job — JobActivity | 1 to 0..* | A job can have zero or many activities, while each job activity belongs to exactly one job. |
| User — JobActivity | 1 to 0..* | A user may author zero or many activities; each activity has exactly one author. |
| Job — Dispute | 1 to 0..* | A job may have zero or many disputes; each dispute belongs to exactly one job. |
| Administrator — Dispute | 0..1 to 0..* | An administrator may resolve zero or many disputes; each dispute has no resolver until it is resolved, then exactly one. |
| WorkSubmission — SubmissionFile | 1 to 1..5 | Each work submission contains 1–5 files, and each submission file belongs to one work submission. |
| WorkSubmission — RevisionRequest | 1 to 0..* | A work submission may receive zero or many revision requests; each request refers to one submission. |
| User — Dispute | 1 to 0..* | A client or assigned freelancer can open many disputes; each dispute is opened by one user. |
| User — Rating (recipient) | 1 to 0..* | A user may receive zero or many ratings; each rating has one recipient. |