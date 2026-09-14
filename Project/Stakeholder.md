# Exercise 4: Identify Project Stakeholders

**Project:** BidBridge, a freelance job board where clients post jobs, freelancers submit competitive bids, and payment is held in escrow until the client approves the delivered work.

| Stakeholder | Role | Interest / Expectations | Influence on the System | How the System Affects the Stakeholder |
|---|---|---|---|---|
| Clients (job posters) | Primary end user who posts jobs, reviews bids, and approves deliverables | Find qualified freelancers at a fair price; be protected from paying for undelivered work | Define the requirements for job posting, bid comparison, and approval features | Reduces hiring risk and gives a structured way to compare offers before committing payment |
| Freelancers (bidders) | Primary end user who browses open jobs and submits bids | Fair access to jobs; assurance of payment after delivery; a visible reputation | Drive the bidding, profile, and rating requirements | Guarantees payment is secured before work begins and builds a reputation over completed jobs |
| Platform administrator | Manages users, moderates job postings, and intervenes in flagged transactions | A system that is easy to monitor and control with minimal manual effort | Determines the administrative dashboard and moderation requirements | Gains centralized oversight tools but takes on responsibility for resolving disputes |
| Development team (students) | Analyze, design, implement, test, and document the system | Deliver a working system on schedule and meet the course learning outcomes | Make all technical and design decisions and control implementation quality | Determines the project grade and provides practical software engineering experience |
| Course / lab instructor | Acts as the customer and evaluator of the project | Correct application of software engineering practices; complete, on-time deliverables | Approves scope and process decisions and sets the evaluation criteria | Provides a project to assess and feedback that redirects the team's work |
| Payment / escrow service provider | External third party that would hold and transfer funds in a real deployment | Compliance with its integration, security, and reporting requirements | Constrains the escrow design and the transaction data model | Would receive transaction volume from the platform in a production version |
