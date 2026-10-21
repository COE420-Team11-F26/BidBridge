# BidBridge — Work Breakdown Structure (WBS)

| ID | Task Name | Description | Predecessor(s) | Duration (Days) |
| --- | --- | --- | --- | --- |
| T1 | Requirements and Database design | Review the FRs, NFRs and use cases and remove any overlaps. Design the database tables and general sketches for the main pages. | — | 14 |
| T2 | Accounts and login | Registration, login for clients, freelancers and admins, password rules, automatic logout after 15 min. | T1 | 6 |
| T3 | Job posting and Bidding | Clients post jobs, freelancers search and submit bids. Clients compare bids and pick the one they want; bids are blocked after the client's deadline. | T2 | 11 |
| T4 | Escrow Payments | A simulated payment service that holds the money when a bid is accepted, releases or refunds it, and records every transaction. | T3 | 8 |
| T5 | Work submission, Messaging, Rating | Freelancers upload completed work and clients approve or ask for a revision. Job messages, 1–5 star rating after completion. | T4 | 8 |
| T6 | Admin and Disputes | Admin moderation over accounts, jobs and payments; disputes resolved by paying or refunding. | T4 | 7 |
| T7 | Integration and Testing | Merge all the parts, test use cases and edge cases, check security and performance. | T5, T6 | 10 |
| T8 | Deployment | Set up the hosting environment and database, deploy the prototype. | T7 | 4 |
| T9 | Documentation | Write the deployment guide, a short user guide and a known-issues list. | T7 | 3 |
