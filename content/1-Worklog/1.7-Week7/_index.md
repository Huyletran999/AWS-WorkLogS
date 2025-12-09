---
title: "Week 7 Worklog"
date: "2025-10-20"
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Week 7 Objectives:
* Design and prototype automated incident response workflows and refine the project architecture based on mentor feedback.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| :-: | :--- | :--------: | :-------------: | :----------------- |
| 3 | - Researching and testing algorithms for ec2 isolation by using SG with no outbound inbound rule | 20/10/2025 | 21/10/2025 | |
| 4 | - Team meeting:<br> &emsp; + Quick AWS Services knowledge revision <br> &emsp; + Conversed about changes in the proposal <br> - Updated AWS Architecture: Added AWS Detective <br> - Revised proposal: <br> &emsp; + Added the usage of AWS Detective <br> &emsp; + Added plan for CDK after finishing the workshop <br> - Mentor recommendations: <br> &emsp; + Visualize data but without using Quicksight, instead make a custom-coded dashboard (Researching) <br> &emsp; + Save GuardDuty findings in S3 bucket for analyzing (Researching) <br> - Successfully configured EventBridge to trigger upon specific GuardDuty findings and: <br> &emsp; + Sent SNS emails to all of team members <br> &emsp; + Triggered a simple Lambda script <br> - Formulated an idea to add to workshop: Make a simple data graphing page hosted in S3 and use API Gateway and Lambda to pull forensics data from Amazon Athena (Researching) | 22/10/2025 | 22/10/2025 | |
| 5 | - Tried out AWS Card Clash with team members: Surprisingly good for learning services and their functions, their placement in Architectures<br> - Reviewed AWS Services Knowledge for Mid-Term: Using Google Gemini to generate quizzes based on the given requirements | 23/10/2025 | 23/10/2025 | [AWS Card Clash](https://aws.amazon.com/training/digital/aws-card-clash/) |
| 6 | - Successfully configured GuardDuty threat list to trigger findings from EC2 Instance activities | 08/15/2025 | 08/15/2025 | [Pháp luật và đạo đức trong công nghệ số](https://www.coursera.org/account/accomplishments/verify/7JELDK2MGGKL) |

### Week 7 Achievements:

* **GuardDuty Hands-on Practice:**
  * Completed the "Getting Hands on with Amazon GuardDuty - AWS Virtual Workshop" and an in-depth lab generated with Amazon Q.
  * Successfully created, tested, and triggered various GuardDuty findings through console settings, EC2 activity, and CloudTrail API access.
  * Established an easier testing environment by successfully triggering sample alerts with different severities and types via CloudShell CLI.
  * Successfully configured a GuardDuty threat list to trigger findings from EC2 Instance activities.

* **Workshop Proposal and Architecture Advancement:**
  * Updated the proposal and AWS Architecture to incorporate AWS Detective for further investigation capabilities.
  * Added a plan for CDK implementation following the completion of the workshop.
  * Initiated research into mentor recommendations, including custom-coded data visualization and saving GuardDuty findings to S3 for analysis.
  * Formulated a new workshop idea for a simple data graphing page hosted in S3 using API Gateway and Lambda.

* **Service Integration and Automation:**
  * Successfully configured EventBridge to act upon specific GuardDuty findings.
  * Automated notifications by sending SNS emails to team members and triggering a Lambda script based on GuardDuty alerts.

* **Network Security Research & Isolation:**
  * Researched and validated algorithms for EC2 isolation by testing Security Groups (SG) with restricted inbound/outbound rules to effectively contain compromised instances.