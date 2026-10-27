# BidBridge — Section 1: Accounts and Administration

**Contributor:** Khalifa Alsuwaidi (b00102801)

## Exercise 1: Individual Class Inventory

| Class ID | Class Name | Purpose / Responsibility | Related Use Case(s) | Contributor |
|---|---|---|---|---|
| S1-C01 | User | Shared account identity, credentials and account status; checks whether login is allowed. | Registration; Login; Account Status | Khalifa Alsuwaidi |
| S1-C02 | Client | Specialized User role for clients; shared with the Job and Bidding section. | Registration; Manage Profile | Khalifa Alsuwaidi |
| S1-C03 | Freelancer | Specialized User role that manages skills and portfolio items. | Registration; Manage Skills; Portfolio | Khalifa Alsuwaidi |
| S1-C04 | Administrator | Specialized User role that performs and records suspend, reactivate, hide and remove actions. | Moderate Accounts / Content | Khalifa Alsuwaidi |
| S1-C05 | UserProfile | Stores public profile details and whether the profile is visible. | View / Update Profile | Khalifa Alsuwaidi |
| S1-C06 | Skill | Represents a reusable skill associated with one or more freelancers. | Manage Freelancer Skills | Khalifa Alsuwaidi |
| S1-C07 | PortfolioItem | Stores a freelancer work sample, its description, link and visibility. | Manage Portfolio | Khalifa Alsuwaidi |
| S1-C08 | ModerationAction | Records the administrator, targeted user, action type, mandatory written reason and date. | Suspend; Reactivate; Hide; Remove | Khalifa Alsuwaidi |
| S1-C09 | AccountService | Handles account registration, authentication and logout; checks account status at login. | Registration; Login; Logout | Khalifa Alsuwaidi |

## Class Selection Justification

These classes represent the main objects needed for P1 and P7 in BidBridge. `User` stores the common account information and tracks whether an account is active, suspended or removed. `Client`, `Freelancer` and `Administrator` inherit from `User` because they share the same account details but have different responsibilities. `UserProfile` stores the profile information, while `Skill` and `PortfolioItem` allow freelancers to show their experience and previous work. `AccountService` handles registration and login and makes sure suspended accounts cannot log in. `ModerationAction` records every suspend, reactivate, hide or remove action with the administrator, the affected user, the date and a required written reason. `User`, `Client`, `Freelancer` and `Administrator` are shared classes that should appear only once in the final team diagram.

## Exercise 2: UML Associations and Multiplicities

| Association | Multiplicity | Explanation |
|---|---|---|
| User — UserProfile | 1 to 1 | Each user has one profile, and each profile belongs to one user. |
| Freelancer — Skill | 0..* to 0..* | Freelancers may list multiple skills; a skill may be listed by many freelancers. |
| Freelancer — PortfolioItem | 1 to 0..* | A freelancer may own many portfolio items; each item belongs to one freelancer. |
| Administrator — ModerationAction | 1 to 0..* | An administrator performs zero or more actions; each action is performed by exactly one administrator. |
| ModerationAction — User | 0..* to 1 | A user can be the target of many actions; every action targets exactly one user. |
| AccountService — User | Dependency | AccountService creates user accounts and authenticates users. |
| Client / Freelancer / Administrator — User | Inheritance | The three roles specialize User and inherit its common account fields and behavior. |

**Constraint:** Every moderation action must include a non-empty written reason.
