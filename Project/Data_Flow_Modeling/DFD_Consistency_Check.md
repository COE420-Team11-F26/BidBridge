# BidBridge — DFD Consistency and Balancing Check

Diagrams: [Context Diagram](Context_Diagram/BidBridge_Context_Diagram.png) · [Level-0 DFD](Level_0_DFD/BidBridge_Level0_DFD.png)

## Processes

| # | Process | Derived from |
| --- | --- | --- |
| 1.0 | Manage User Accounts | FR-03 (M), FR-11, FR-15 · UC-06, UC-10, UC-16 |
| 2.0 | Manage Job Postings | FR-01 (M), FR-04 (M), FR-17 · UC-17, UC-19 |
| 3.0 | Process Bids | FR-02 (M), FR-12, FR-13, FR-16, FR-18, FR-01 (E) · UC-07, UC-08, UC-11, UC-12, UC-18 |
| 4.0 | Manage Work Delivery | FR-02 (E), FR-03 (E), FR-14, FR-05 (M) · UC-02, UC-03, UC-09, UC-20 |
| 5.0 | Handle Escrow Payments | FR-01 (E), FR-04 (E), FR-20 · UC-01, UC-04, UC-15 |
| 6.0 | Resolve Disputes | FR-05 (E) · UC-05 |
| 7.0 | Moderate Platform | FR-19 · UC-13, UC-14 |

(E) = Emran's FRs, (M) = Mohamed's FRs; FR-11 to FR-20 are numbered uniquely.

## Data stores

| ID | Data store | Contents |
| --- | --- | --- |
| D1 | Users | Accounts, credentials, roles, profiles/portfolios, account status |
| D2 | Jobs | Job postings, deadlines, accepted bid, job status (Open → Assigned → Submitted → Completed), visibility |
| D3 | Bids | Bid price, delivery time, proposal, bid status |
| D4 | Job Activity | Work submissions (files, notes), job messages, star ratings |
| D5 | Transactions | Escrow holds, releases, refunds (job ID, amount, payer, payee, timestamp) |
| D6 | Disputes | Dispute reason, parties, status, resolution |

D1 and D2 are drawn more than once (marked with an extra line in the ID box) so that no flow lines cross; the Platform Administrator entity is also drawn twice (diagonal corner mark).

## Balancing with the Context Diagram

All 32 external flows of the Context Diagram appear on the Level-0 DFD with the same names, entities and directions, and no new external flows were added.

| External entity | Flow (Context Diagram) | Direction | Level-0 process |
| --- | --- | --- | --- |
| Client | Registration, login & profile details | In | 1.0 |
| Client | Job posting details | In | 2.0 |
| Client | Bid acceptance | In | 3.0 |
| Client | Work approval / revision request | In | 4.0 |
| Client | Job messages & freelancer rating | In | 4.0 |
| Client | Dispute request | In | 6.0 |
| Client | Login result & account status | Out | 1.0 |
| Client | New-bid notifications & sorted bid list | Out | 3.0 |
| Client | Submitted work files & notification | Out | 4.0 |
| Client | Freelancer messages | Out | 4.0 |
| Client | Transaction history & refund notice | Out | 5.0 |
| Freelancer | Registration, login & portfolio details | In | 1.0 |
| Freelancer | Job search keywords | In | 2.0 |
| Freelancer | Bid proposal / edit / withdrawal | In | 3.0 |
| Freelancer | Work submission (files & note) | In | 4.0 |
| Freelancer | Job messages & client rating | In | 4.0 |
| Freelancer | Dispute request | In | 6.0 |
| Freelancer | Login result & account status | Out | 1.0 |
| Freelancer | Matching open jobs | Out | 2.0 |
| Freelancer | Bid status, history & job assignment | Out | 3.0 |
| Freelancer | Revision requests & client messages | Out | 4.0 |
| Freelancer | Payment release notice & transaction history | Out | 5.0 |
| Platform Administrator | Admin login credentials | In | 1.0 |
| Platform Administrator | Moderation action & reason | In | 7.0 |
| Platform Administrator | Dispute resolution decision (pay / refund) | In | 6.0 |
| Platform Administrator | Login result | Out | 1.0 |
| Platform Administrator | Reported accounts & job postings | Out | 7.0 |
| Platform Administrator | Open dispute cases | Out | 6.0 |
| Payment / Escrow Service | Escrow hold confirmation | In | 5.0 |
| Payment / Escrow Service | Transfer confirmation | In | 5.0 |
| Payment / Escrow Service | Escrow hold request | Out | 5.0 |
| Payment / Escrow Service | Release / refund instruction | Out | 5.0 |
