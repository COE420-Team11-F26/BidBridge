\# BidBridge — Non-Functional Requirements



\## Individual Contributions



\### Emran Lotfi



| NFR ID | Category | Non-Functional Requirement | Contributor |

| --- | --- | --- | --- |

| NFR-01 | Security | Only the client who owns a job shall be able to approve its work or release its escrow; any such request from another user shall be rejected and written to the audit log. | Emran Lotfi |

| NFR-02 | Reliability | Escrow release and the job status change to Completed shall execute as one atomic transaction: if either step fails, both are rolled back, so no job is ever Completed without a matching release record. | Emran Lotfi |

| NFR-03 | Performance | Accepting a bid (including creating the escrow hold) shall complete within 3 seconds for 95% of requests with 50 concurrent users. | Emran Lotfi |

| NFR-04 | Usability | A client shall be able to reach and approve a submitted deliverable in at most 3 clicks from their dashboard; at least 4 of 5 first-time test users shall complete this without help. | Emran Lotfi |

| NFR-05 | Maintainability | All payment logic shall be isolated behind a single PaymentService interface, so the simulated escrow can be replaced by a real provider without changing the job or bid modules; the escrow module shall have at least 80% unit-test coverage. | Emran Lotfi |





\### Mohamed ElZefzafy



| NFR ID | Category | Non-Functional Requirement | Contributor |

| --- | --- | --- | --- |

| NFR-06 | Performance | The system will display search results for project and task listings in under 2 seconds with 50 active users on the site. | Mohamed ElZefzafy |

| NFR-07 | Security | The users both Clients and Freelancers will be automatically logged out after 15 minutes of inactivity to prevent unauthorized access. | Mohamed ElZefzafy |

| NFR-08 | Portability | The application will run without any layout errors or feature loss on standard desktop and mobile phones. | Mohamed ElZefzafy |

| NFR-09 | Scalability | The system database shall execute queries under 0.5s when storing 20,000 tasks. | Mohamed ElZefzafy |

| NFR-10 | Security | The registration system shall limit account creation requests to a maximum of 5 attempts per IP address per hour to prevent bot and automatic sign ups. | Mohamed ElZefzafy |





\### Marwan Ahmed



| NFR ID | Category | Non-Functional Requirement | Contributor |

| --- | --- | --- | --- |

| NFR-11 | Security | User passwords shall not be stored as plain text and shall be stored using a secure password-hashing method. | Marwan Ahmed |

| NFR-12 | Performance | The system shall display the list of bids for a job within 2 seconds for at least 95% of requests when the job contains up to 100 bids and the system has up to 50 active users. | Marwan Ahmed |

| NFR-13 | Reliability | The system shall ensure that only one bid can be accepted for a job, even if two acceptance requests are received at almost the same time. | Marwan Ahmed |

| NFR-14 | Usability | Forms for login, profile editing, and bid editing shall clearly identify invalid or missing fields before submission and shall preserve correctly entered information when an error occurs. | Marwan Ahmed |

| NFR-15 | Robustness | Invalid input, duplicate requests, or unsupported values shall be rejected without causing the application to crash or changing previously stored valid data. | Marwan Ahmed |





\### Khalifa Alsuwaidi



| NFR ID | Category | Non-Functional Requirement | Contributor |

| --- | --- | --- | --- |

| NFR-16 | Availability | The BidBridge web application shall maintain at least 99.5% availability per month, excluding scheduled maintenance periods announced in advanced | Khalifa Alsuwaidi |

| NFR-17 | Recoverability | The system database shall be backed up automatically at least once every 24 hours, and the latest successful backup shall be restorable within 60 minutes following a database failure | Khalifa Alsuwaidi |

| NFR-18 | Auditability | Administrative moderation actions and changes to payment status shall be recorded in an audit log containing the acting user ID,action performed, affected account or job and timestamp. Audit records shall be retained for at least 90 days | Khalifa Alsuwaidi |

| NFR-19 | Usability | Core BidBride pages including login, job browsing, job posting, bidding and dashboards shall support keyboard navigation and properly labeled controls. | Khalifa Alsuwaidi |

| NFR-20 | Security | All communications containing login credentials, personal information, or payment related information between the user’s browser and the BidBridge server shall be transmitted using HTTPS with TLS 1.2 or later. | Khalifa Alsuwaidi |



