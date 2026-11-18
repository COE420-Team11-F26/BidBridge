# Architectural Design Goals

| Goal ID | Design goal | Description | Related Requirements | Priority | Justification |
|---|---|---|---|---|---|
| G01 | Security | Protect accounts, passwords and payment info | NFR-01, NFR-07, NFR-10, NFR-11, NFR-20 | High | BidBridge holds user accounts and escrow money, so they need to be protected. |
| G02 | Reliability | Payments and job status must stay in sync. | NFR-02 | High | A job should never be Completed unless its payment was released. |
| G03 | Availability | The system should stay up and be recoverable after a failure. | NFR-16, NFR-17 | Medium | Users need to be able to use BidBridge whenever they want, and the data must be restorable if the database fails. |
| G04 | Performance | Search, bid lists and accepting a bid should be fast. | NFR-03, NFR-06, NFR-12 | Medium | Our NFRs set time limits for them: 2 seconds for search and bid lists, 3 seconds for accepting a bid. |
