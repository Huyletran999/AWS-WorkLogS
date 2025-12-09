---
title: "Week 10 Worklog"
date: "2025-11-10"
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---
### Week 10 Objectives:

* Fully research and test all components to prepare for integrating them into the final workshop build.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| :-: | :--- | :--------: | :-------------: | :----------------- |
| 2 | - Tested EC2 isolation with mock events and real GuardDuty findings (debugged and fixed data parsing functions to accommodate real finding JSON structures).<br> - Updated proposal:<br>&emsp; + Included updated AWS Architecture and Services.<br>&emsp; + Recalculated pricing estimates. | 10/11/2025 | 10/11/2025 | |
| 3 | - Tested IAM quarantine and currently tackling similar data parsing problems.<br> - Successfully built all policies and roles with least-privilege access. | 11/11/2025 | 11/11/2025 | |
| 4 | - Successfully built Step Functions designs including states for: Check Finding Types, Isolate EC2, Quarantine Users, and No Action Needed. | 12/11/2025 | 12/11/2025 | |
| 5 | - Successfully tested Lambda functions with both mock events and some real findings using the new scripts.<br> - Currently aiming to build scripts capable of parsing every finding type.<br> - Researching how to optimize the Lambda -> EventBridge -> Step Functions structure. | 13/11/2025 | 13/11/2025 | |

### Week 10 Achievements:

* **Incident Response Orchestration:**
  * Successfully designed and deployed the AWS Step Functions workflow, featuring distinct logical states for "Check Finding Types," "Isolate EC2," "Quarantine IAM User," and "No Action Needed."
  

* **Real-world Testing & Debugging:**
  * Transitioned from testing with mock events to handling real Amazon GuardDuty findings.
  * Successfully debugged and refined the Lambda data parsing logic to correctly interpret the complex JSON structure of actual GuardDuty alerts for both EC2 and IAM scenarios.

* **Security & IAM Implementation:**
  * Successfully architected and deployed all necessary IAM roles and inline policies for the quarantine functions, strictly adhering to **least-privilege access** principles to ensure security best practices.

* **Project Documentation & Optimization:**
  * Updated the project proposal to reflect the shift to Step Functions architecture and provided recalculations for projected cloud costs.
  * Initiated research into optimizing the integration pattern between AWS EventBridge and Step Functions to ensure faster and more reliable automated triggers.