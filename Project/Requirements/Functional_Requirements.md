\# BidBridge — Functional Requirements



\## Individual Contributions



\### Emran Lotfi



| FR ID | Functional Requirement | Source Scenario/Stakeholder | Contributor |

| --- | --- | --- | --- |

| FR-01 | When a client accepts a bid, the system shall hold an escrow amount equal to the accepted bid price and shall change the job status from Open to Assigned only after the hold succeeds. | S-03 / Client, Payment provider | Emran Lotfi |

| FR-02 | The system shall allow the assigned freelancer of an Assigned job to submit work by uploading 1–5 files (max 25 MB each) with a submission note, and shall then change the job status to Submitted and notify the client. | S-04 / Freelancer | Emran Lotfi |

| FR-03 | The system shall allow the client of a Submitted job to either approve the work or request a revision; a revision request shall require a written comment and shall return the job status to Assigned. | S-04 / Client | Emran Lotfi |

| FR-04 | When the client approves the work, the system shall release the escrowed amount to the freelancer's platform balance, set the job status to Completed, and record a transaction (job ID, amount, payer, payee, timestamp). | S-04 / Freelancer, Client | Emran Lotfi |

| FR-05 | The system shall allow the client or freelancer of an Assigned or Submitted job to open a dispute with a reason; opening a dispute shall freeze the escrow so it cannot be released until an administrator resolves it by paying the freelancer or refunding the client. | S-05 / Client, Freelancer, Administrator | Emran Lotfi |





\### Mohamed ElZefzafy



| FR ID | Functional Requirement | Source Scenario/Stakeholder | Contributor |

| --- | --- | --- | --- |

| FR-01 | The system will allow Clients to create a task posting, specifying its title, description, and bid deadline date. | Client posts a design job, Client Stakeholder | Mohamed ElZefzafy |

| FR-02 | The system will allow freelancers to submit bid proposals for eligible tasks, that contain their bid price, completion time, and information about themselves and their skills. | Freelancer bids on a job, Freelancer Stakeholder | Mohamed ElZefzafy |

| FR-03 | The system will allow new clients and new freelancers to register and sign up by entering their email address and a password, and selecting either ‘Client’ or ‘Freelancer’ | Clients and Freelancer Stakeholders | Mohamed ElZefzafy |

| FR-04 | The system will allow freelancers to search for task postings using keywords from the task title and skills required. | Freelancer Stakeholder | Mohamed ElZefzafy |

| FR-05 | The system will allow both Clients and Freelancers to submit a star rating from 1-5 for each other upon completion. | Clients and Freelancer Stakeholders | Mohamed ElZefzafy |





\### Marwan Ahmed



| FR ID | Functional Requirement | Source Scenario/Stakeholder | Contributor |

| --- | --- | --- | --- |

| FR-11 | The system shall allow registered clients, freelancers, and administrators to log in using their email address and password. If the login information is incorrect, the system shall reject the login attempt and display an error message. | S-05 / Client, Freelancer, Administrator | Marwan Ahmed |

| FR-12 | The system shall allow a client to view all bids submitted for their open job and sort the bids by bid price, delivery time, or freelancer rating. | S-03 / Client | Marwan Ahmed |

| FR-13 | The system shall allow a freelancer to edit the bid price and proposed delivery time, or withdraw their bid, as long as the job is still Open and the bid has not been accepted. | S-02 / Freelancer | Marwan Ahmed |

| FR-14 | The system shall allow the client and the assigned freelancer to exchange text messages related to an active job, and each message shall display the sender and timestamp. | S-04, S-05 / Client, Freelancer | Marwan Ahmed |

| FR-15 | The system shall allow users to update their profile information. Freelancers shall also be able to add their skills, short biography, and portfolio information to their profile. | Client, Freelancer | Marwan Ahmed |





\### Khalifa Alsuwaidi



| FR ID | Functional Requirement | Source Scenario/Stakeholder | Contributor |

| --- | --- | --- | --- |

| FR-16 | When a freelancer submits a new bid on a job, system will notify the client who owns the job and display the job title,freelancer name,bid price and time of submission | Client | Khalifa Alsuwaidi |

| FR-17 | The system will prevent freelancers from submitting new bids after a job’s bidding deadline has passed. If no bid has been accepted by deadline, the system shall stop accepting bids and update the job so that it is no longer available for bidding. | Client, Freelancer | Khalifa Alsuwaidi |

| FR-18 | The system shall allow a freelancer to view a list of all bids they have submitted, including the related job,bid amount, proposed delivery time and current bid status such as pending, accepted, rejected or withdrawn. | Freelancer, Stakeholder | Khalifa Alsuwaidi |

| FR-19 | The system will allow a platform administrator to suspend or reactivate user accounts and remove or hide job postings that violate platform rules. The administrator shall be required to enter a reason for each moderation action | Platform, Administrator, Stakeholder | Khalifa Alsuwaidi |

| FR-20 | The system shall allow clients and freelancers to view their transaction history,including the related job ID, transaction amount,payment status, transaction type, and timestamp | Client, Freelancer, Payment provider | Khalifa Alsuwaidi |

