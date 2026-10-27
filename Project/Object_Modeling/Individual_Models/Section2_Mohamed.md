# Part A: Section 2 Class Inventory (Jobs, Bidding, & Notifications)
**Contributor:** Mohamed ElZefzafy

| Class ID | Class Name | Purpose / Responsibility | Related Use Case(s) | Contributor |
| :--- | :--- | :--- | :--- | :--- |
| S2-C01 | Job | Stores a posted job (title, description, skills, bid deadline, status). Checks if it accepts bids and records accepted bids. | UC-01, UC-07, UC-17, UC-19 | Mohamed ElZefzafy |
| S2-C02 | Bid | Stores a freelancer's offer (price, delivery time, status). Can only be edited or withdrawn while the job is open. | UC-01, UC-07, UC-08, UC-12, UC-18 | Mohamed ElZefzafy |
| S2-C03 | Notification | Stores a message sent to a user (e.g., new bid, submitted work) and its timestamp. | UC-02, UC-11 | Mohamed ElZefzafy |
| S2-C04 | JobSearch | Searches open jobs by keyword, matching the title and required skills. | UC-19 | Mohamed ElZefzafy |
| S2-C05 | BidHistory | Lists a freelancer's submitted bids with job, amount, delivery time, and status. | UC-12 | Mohamed ElZefzafy |

### Class Selection Justification
These classes represent the main objects needed for jobs, bidding, and notifications in BidBridge. Job stores a posted job with its title, description, skills, deadline, and status, checking if the job still accepts bids. Bid stores a freelancer's offer price with delivery time and status, editable/withdrawable only while the job remains open. Notification alerts users when bids are placed/accepted or work is submitted. JobSearch handles keyword matching for freelancers searching open jobs. BidHistory tracks submitted bids per freelancer. Shared classes (User, Client, Freelancer, Escrow) connect Section 2 to the rest of the system.
