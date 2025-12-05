---
title: "Week 12 Worklog"
date: "2025-11-24"
weight: 2
chapter: false
pre: " <b> 1.12. </b> "
---
### Week 12 Objectives:

* Initialize and validate the Infrastructure as Code (CDK) environment.
* Enhance the Incident Response workflow with automated forensics collection (SSM).
* Debug and refine Lambda functions and IAM roles for reliable execution.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| :-: | :--- | :--------: | :-------------: | :----------------- |
| 2 | - Successfully installed AWS CDK with AWS CLI<br> - Completed the tutorial for creating a first application with CDK: <br>&emsp; + Deployed stacks on AWS Accounts <br>&emsp; + Used `diff` to compare changes <br>&emsp; + Destroyed stack after finishing <br> - Created a Github Organization for the team | 25/11/2025 | 25/11/2025 | [CDK Tutorial](https://docs.aws.amazon.com/cdk/v2/guide/hello-world.html) |
| 3 | - **IR Step Functions update:** Added a **Map State** to iterate over isolated Instances and trigger an SSM Lambda for those Instances to collect logs for forensics.<br> - **CDK:** Moved the CDK testing environment to a new dedicated account. | 26/11/2025 | 26/11/2025 | |
| 6 | - **Team meetings:**<br>&emsp; + Assigned CDK tasks for members <br>&emsp; + Got started on updating proposal and architecture diagram <br> - **Fixed and improved IR Step Functions:** <br>&emsp; + Fixed `EC2Isolate` Lambda: Corrected parsing method <br>&emsp; + Improved state: Added Parsing Lambda and reordered functions <br>&emsp; + SSM Failed due to missing IAM: Added necessary roles to the SSM Forensics Function. | 28/11/2025 | 30/11/2025 | |

### Week 12 Achievements:

* **Infrastructure as Code (IaC) Initialization:**
  * Successfully installed and configured **AWS CDK** with the CLI.
  * Mastered the fundamental CDK lifecycle by deploying, diffing, and destroying stacks in a live environment.
  * Established a **GitHub Organization** to centralize team repositories and manage the migration to CDK.

* **Incident Response & Forensics Logic:**
  * Enhanced the Step Functions workflow by implementing a **Map State**, enabling the system to iterate through multiple isolated EC2 instances simultaneously.
  
  * Integrated an **SSM (Systems Manager) Lambda** to automatically trigger forensic log collection on compromised instances.

* **Debugging & Optimization:**
  * Refined the data handling logic by fixing JSON parsing errors in the `EC2Isolate` Lambda.
  * Resolved permission issues by attaching the correct **IAM Roles** to the SSM Forensics function, ensuring it has permission to execute commands on EC2 instances.
  * Optimized the workflow structure by reordering states and adding a dedicated Parsing Lambda for better data flow.