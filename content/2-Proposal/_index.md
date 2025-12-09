---
title: "Proposal"
date: "2000-01-01"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

![AWS Logo](/images/2-Proposal/image.png)

# FCJ Internship Project Proposal

# Automated AWS Incident Response and Forensics System

**Prepared by:** The Ballers – FPT University  
**Date:** December 5, 2025  
**Program:** AWS First Cloud Journey (FCJ) Internship  
**Project Duration:** 6 Weeks  
**Status:** Ready for Review & Approval <br>
**Proposal Link:** [Proposal](https://docs.google.com/document/d/1RcPJmiVxS80qdi0wOvHltBcSoZtRC97LngEZEkKC09k/edit?brid=hv-MPz2j8n_U1ZiCdslbyw&tab=t.0) 

## Table of Contents

1. [Background and Motivation](#1-background-and-motivation)
2. [Solution Architecture](#2-solution-architecture--architectural-diagram)
3. [Activities and Deliverables](#3-activities-and-deliverables)
4. [Expected AWS Cost Breakdown by Services](#4-expected-aws-cost-breakdown-by-services)
5. [Team](#5-team)
6. [Resources & Cost Estimates](#6-resources--cost-estimates)
7. [Acceptance](#7-acceptance)

## 1. Background and Motivation

### 1.1 Executive Summary

Our team is building an automated incident response and forensics solution as part of the AWS First Cloud Journey internship program. The idea is straightforward—when a security issue happens in AWS, we want the system to respond automatically without waiting for manual intervention.

We're creating a platform that automatically detects security findings from GuardDuty, isolates affected resources, captures forensic evidence through comprehensive data collection, and provides analytics and dashboards where security teams can investigate what happened. Everything is built using Infrastructure-as-Code with AWS CDK, so customers can easily deploy it into their own AWS accounts.

The main use cases include detecting unauthorized AWS credential use, identifying compromised EC2 instances, and ensuring forensic data is properly collected, processed, and stored for investigation. Our architecture integrates VPC Flow Logs, CloudTrail, and GuardDuty to detect threats, while Step Functions orchestrates the automated response workflow including EC2 isolation, ASG detachment, and IAM quarantine. All evidence is collected and processed through custom ETL Lambda and Data Firehose, using Athena for forensic analysis.

### 1.2 Project Success Criteria

We measure success through these key objectives:

* Successfully deploy a fully functional incident response orchestrator that customers can use immediately after installation
* Reduce investigation time from hours to minutes by automating evidence collection and response
* Ensure all forensic evidence is properly collected, processed, and stored
* Deliver everything on schedule within our 6-week timeline
* Keep deployment costs under $5/month for typical usage
* Enable all team members to demonstrate competency in AWS security services, serverless architecture, forensics collection, and web application protection.

### The Problem We Want to Solve

The increasing frequency and sophistication of cyber threats pose significant risks to organizations relying on cloud infrastructure. Manual incident response processes are often slow, inconsistent, and prone to human error, which can lead to prolonged system downtime, data breaches, and financial losses. The project aims to address these challenges by developing an automated, reliable, and scalable incident response system that minimizes response time, enhances forensic capabilities, and reduces operational costs.

### Benefits

* Rapid threat detection and automated response reduce the window of vulnerability.
* Automated forensic data collection ensures comprehensive evidence gathering, facilitating faster investigations.
* Cost-effective deployment leveraging AWS serverless services minimizes infrastructure expenses.
* Improved security posture through continuous monitoring and real-time alerts.
* Empowers security teams with actionable insights via dashboards and analytics.
* Scalable architecture adaptable to organizations of various sizes and incident volumes.

### 1.3 Assumptions

**Customer Assumptions:**

* Customers have an AWS account with appropriate permissions to deploy our CDK application.
* Customers have basic familiarity with AWS services and can run simple CLI and CMD commands.
* GuardDuty is already enabled or customers are willing to enable it as part of setup.
* Customers want a self-contained solution for the initial deployment.
* The team has consistent access to AWS during the 6-week project period.

**Dependencies and Constraints:**

* Our solution integrates with AWS native services only (at the moment).
* Forensics collection includes VPC Flow Logs, DNS Logs, CloudTrail, and EC2 snapshot.
* We use services available on the free tier or low-cost services (Lambda, Step Functions, Data Firehose, Athena).
* All infrastructure is defined in AWS CDK (Python) for reproducible deployment.
* Dashboard is static S3-hosted with Cognito authentication, CloudFront CDN.
* We follow AWS Well-Architected Framework principles throughout.

### Risk Mitigation

To address the potential challenges associated with implementing AWS services and forensic data processing at scale, a comprehensive risk mitigation plan should be adopted. This plan includes the following measures:

* **Training and Skill Development:** Beyond initial training, establish ongoing education programs and certifications for team members to stay updated with AWS advancements and best practices. This reduces the learning curve and enhances operational efficiency.
* **Robust Performance Optimization:** Regularly review and fine-tune Athena queries and Data Firehose configurations. Implement automated monitoring tools to detect performance bottlenecks early and adjust resources dynamically to maintain optimal throughput.
* **Data Security and Compliance:** Incorporate strict security protocols, including encryption, access controls, and audit logging, to safeguard sensitive forensic data. Ensure compliance with relevant regulations such as GDPR, HIPAA, or industry-specific standards.
* **Disaster Recovery and Business Continuity:** Develop and test disaster recovery plans that include data backups, failover procedures, and redundancy measures to minimize downtime and data loss during failures.
* **Scalability Planning:** Anticipate future data growth and workload increases by designing scalable architecture. Use auto-scaling features and cost management tools to optimize resource utilization and control expenses.
* **Vendor and Technology Evaluation:** Continuously evaluate AWS service updates and alternative solutions to ensure the chosen tools remain effective and cost-efficient as requirements evolve.

Implementing these enhanced risk mitigation strategies will provide a more resilient framework for managing the complexities of forensic data processing and cloud service deployment, ultimately reducing operational risks and ensuring data integrity and security.

## 2. Solution Architecture / Architectural Diagram

### 2.1 Technical Architecture Diagram

![AWS Architecture](/images/2-Proposal/AWSWorkshopArchitecture-Stepfunctions.drawio.png)

Our solution uses a comprehensive multi-stage architecture for automated incident response and forensics:

#### Data Collection & Detection Layer

The system collects security events from multiple sources:

* **VPC Flow Logs and DNS Logs** from network interfaces capture network traffic patterns.
* **CloudTrail** logs all AWS API calls and management activities.
* **EC2 Instances** generate system-level telemetry.
* **GuardDuty** continuously monitors for security threats and suspicious activity.
* **CloudWatch** collects metrics and logs from AWS resources.

#### Event Processing Layer

When GuardDuty detects a finding:

* **Event Bridge** routes findings to our Step Functions.
* Events are classified by type to determine response action.

#### Automated Response Orchestration (Step Functions Workflow)

Our Step Functions state machine orchestrates the incident response with these sequential actions:

1. **Parse Findings** - Extract critical information from security event.
2. **Finding Type** - Decision point to determine response strategy.
3. **Isolate EC2** - Remove compromised instance from production and isolate them.
4. **Termination Protection & Tagging** - Protect instance and tag for forensics.
5. **Detach ASG** - Detach from Auto Scaling Group.
6. **Create Snapshot** - Capture EBS volume for forensic analysis.
7. **Quarantine IAM** - Isolate credentials and permissions.

#### Alerting & Notification Layer

* **Amazon SNS** distributes alerts to multiple channels.
* **Alert Dispatch** routes notifications appropriately.
* **Simple Email Service (SES)** sends email notifications.
* **Third-party messaging platform (Slack)** delivers real-time alerts to security teams.

#### Data Processing & Analytics Layer

Collected forensic data flows through:

* **CloudWatch** logs for immediate analysis.
* **Raw Log Data** stored in S3 for long-term retention.
* **DATA ETL** pipeline processes raw data.
* **Data Firehose** streams processed data to S3 bucket.
* **Processed Data** storage for normalized forensic information.
* **Athena** enables SQL queries against forensic datasets.

#### Dashboard & Analysis Layer

Security analysts access investigation tools through:

* **Dashboard Query** interface for investigations.
* **API Gateway** provides programmatic access to forensic data.
* **Athena** delivers real-time SQL query results.
* **S3 Static Dashboard** provides visual investigation interface.
* **Cognito** handles authentication and authorization.
* **CloudFront** CDN accelerates dashboard delivery.

**Output & Notification:**

* Final alerts and findings are sent to **Slack and Email**.
* **Users** (security team) receive actionable intelligence for investigation.

### 2.2 Technical Plan

Our team develops the entire solution using AWS Cloud Development Kit (CDK) with Python. CDK allows us to write infrastructure as code, enabling version control, testing, and easy customization by customers.

**Approach:**

Create a CDK project with modular constructs representing each architectural layer:
* Detection layer (GuardDuty, CloudWatch, EventBridge integration, CloudTrail).
* Orchestration layer (Step Functions, Lambda functions for each action).
* Data collection layer (Data Firehose, S3 storage, ETL processes).
* Analytics layer (Athena, dashboards, API Gateway, CloudFront).
* Notification layer (SNS, SES, third-party integrations).

**Step Functions Workflow:**
* State machine with decision logic based on finding type.
* Findings trigger immediate containment (EC2 isolation, ASG detachment, IAM quarantine).

**Step Functions:**
Written in Python for AWS SDK compatibility.

Specific responsibilities:
* **Parse Findings (Lambda)** - Extract and normalize GuardDuty data.
* **Isolate EC2 (Lambda)** - Modify security groups and remove from load balancers.
* **Protect Instance** - Set termination protection and forensic tags.
* **Detachment from ASG** - Detach instance from auto scaling group.
* **Create Snapshot** - Initiate EBS snapshot for forensic analysis.
* **Quarantine IAM (Lambda)** - Apply restrictive policies to compromised credentials.

Separation of concerns enables easy testing and independent updates.

**Data Collection Pipeline:**
* Logs exported from CloudWatch and CloudTrail.
* Lambda-based ETL normalizes data formats.
* Data Firehose streams processed forensic data to S3 with automatic partitioning.
* Athena tables created for efficient SQL queries.

**Dashboard Development:**
* Static S3-hosted HTML/CSS/JavaScript (React) interface.
* Cognito integration for authentication.
* API Gateway connects dashboard to Lambda functions.
* Real-time query results from Athena.
* CloudFront CDN caches dashboard and query results.

**Testing:**
* Integration tests simulating real GuardDuty findings.
* End-to-end tests validating complete response workflows.

---

### 2.3 Project Plan

We use Agile Scrum with 1-week sprints over 6 weeks (6 sprints total).

**Sprint 1:**
* Team training on GuardDuty, Step Functions, Data Firehose, Athena.
* Architecture design review with AWS mentor.
* VPC and security group setup.

**Sprint 2:**
* Implement Step Functions workflow with all orchestration logic.
* Develop Lambda functions for each response action.
* Integrate GuardDuty and EventBridge.
* Set up SNS and SES for notifications.
* Integration testing of incident response flows.
* Deliverable: End-to-end working orchestration responding to security findings.

**Sprint 3:**
* Create S3-based forensic data storage.
* Develop Athena tables and queries for forensic analysis.
* Implement ETL data processing.
* Deliverable: Functional forensic data collection and analysis pipeline.

**Sprint 4:**
* Build static S3-hosted dashboard interface.
* Create API Gateway connections to backend functions.
* Integrate Athena query results into dashboard.
* Set up CloudFront CDN.
* Deliverable: Working dashboard.

**Sprint 5:**
* Implement Cognito authentication.
* Performance testing of data pipelines and queries.
* Simulated incident scenarios.
* Manual testing and bug fixes.
* Implement Firehose for optimization.
* Optimize Athena queries.

**Sprint 6 (Documentation & Handover):**
* Create deployment guides.
* Record video demonstrations.
* Knowledge transfer sessions.
* Deliverable: Complete documentation and public GitHub and GitLab repository.

**Sprint Ceremonies:**
* Semiweekly 30-minute standups for progress synchronization.
* Weekly sprint reviews showing completed work.
* Retrospectives to discuss what went well and improvement areas.

---

### 2.4 Security Considerations

We implement security across five key dimensions:

**Access Control:**
* Every Lambda function gets only specific permissions needed for its action.
* Careful IAM role and policy management with least privilege.
* Cognito authentication for dashboard access.

**Infrastructure Security:**
* Infrastructure in private VPC subnets where possible.
* Security groups restricting traffic between components.
* VPC Flow Logs for network visibility.
* GuardDuty for real-time threat detection in logs.
* CloudTrail logging every API call for complete audit trails.
* EventBridge rules validated and restricted.

**Data Protection:**
* AES-256 encryption for all forensic evidence in S3.
* TLS 1.2+ for all data transfers between services.
* Encryption in transit for Data Firehose streams.

**Detection & Monitoring:**
* CloudWatch monitoring Lambda functions, Step Functions executions, and metrics.
* Custom dashboards for real-time incident tracking.
* Athena query logging for audit trails.

**Incident Response:**
* Automatic EC2 isolation when security findings occur.
* Forensic evidence captured immediately.
* Complete chain of custody with timestamped logs.
* IAM credential quarantine.
* Notifications to security team through Slack and Email.
* Evidence retention for investigation period.

## 3. Activities and Deliverables

### 3.1 Activities and Deliverables

| Project Phase | Timeline | Activities | Deliverables |
| :--- | :--- | :--- | :--- |
| **Foundation & Setup** | Week 6-7 | CDK project setup with modular constructs, team training on GuardDuty/Step Functions/Firehose, architecture design review, VPC and security setup. | Working CDK project repository, architecture document v1, team training completion, GitHub repository established. |
| **Core Orchestration** | Week 7-9 | Step Functions workflow development, Lambda function coding for all response actions, EventBridge integration, SNS/SES setup, integration testing. | Step Functions state machine definition, 7+ Lambda functions with documentation, GuardDuty integration, notification system, API Gateway. |
| **Data & Analytics** | Week 10 | Data Firehose deployment, S3 forensic storage setup, Athena table creation, ETL pipeline development, SQL query library. | Data Firehose pipeline, 15+ Athena queries documented, forensic analysis runbooks, processed data storage. |
| **Dashboard & UI** | Week 11 | Static dashboard development, Cognito authentication, API Gateway setup, CloudFront CDN configuration, dashboard integration. | S3-hosted dashboard, authentication system, query interface, real-time results integration. |
| **Testing & Validation** | Week 12 | Manual testing, security scanning including simulated incident scenarios (5+ workflows), performance testing, attack simulation. | Security scan results, incident simulation videos. |
| **Documentation & Handover** | Week 13 | Deployment guide, API documentation, knowledge transfer sessions, final demo, GitHub cleanup. | Complete GitHub repository (public), deployment guide instructions, live workshop demonstration. |

**Governance:**

* GitHub and GitLab for version control with complete commit history.
* Meetings with AWS FCJ members and mentors for architecture reviews.
* Weekly sprint reviews with stakeholders (our team).
* Risk register updated Semiweekly during standups.

---

### 3.2 Out of Scope

These items are NOT included in our project:

* Forensics for resources outside of AWS (on-premise servers, user computers).
* Legal advice or formal certification about evidence admissibility in court.
* Integration with ticketing systems (ServiceNow, Jira) - initial deployment only.
* Load testing for tens of thousands of simultaneous incidents.
* Machine learning models for threat prediction.
* Compliance certifications (PCI-DSS, ISO 27001) - design follows principles but not certified.
* WAF
* Lambda@Edge (only available to pay-as-you-go plans).
* Multi-region disaster recovery automation.
* Advanced Cognito with MFA – basic authentication only.
* Advanced DDoS protection (AWS Shield Advanced) - standard protection only.
* Glue ETL Jobs and Crawler.
* Third-party security services.

### 3.3 Path to Production

We're delivering a production-ready proof-of-concept and foundation for incident response automation. It's fully functional for demonstration, workshops, and small-to-medium deployments.

For large enterprise deployment, customers would additionally need:

* Automated escalation procedures and on-call rotation integration.
* Enterprise ticketing system integration (ServiceNow, Jira).
* Additional messaging platform connections (Teams, PagerDuty).
* Optimization for massive incident volumes per day.
* Multi-region failover and disaster recovery capabilities.
* Advanced forensic tool integrations.
* Compliance validation and regulatory mapping (HIPAA, GDPR, PCI-DSS).
* SIEM integration for centralized logging.
* AWS WAF Premium features (bot control, advanced threat intelligence).
* Advanced WAF logging and analytics integration.
* AWS Shield Advanced DDoS

We're designed as a foundation that's easy to build upon.

## 4. Expected AWS Cost Breakdown by Services

Here's a typical monthly deployment cost breakdown using the free tier:

[**Estimate Pricing**](https://calculator.aws/#/estimate?id=b9b2c0423dcd3b21dadd62e5053a5fdf2d003339)

| AWS Service | Monthly Cost | Why We Use It | Region |
| :--- | :---: | :--- | :--- |
| **Lambda** | $0-1 | Runs our automation functions | Asia Pacific (Singapore) |
| **SES** | $0.09-1 | Sends Email | Asia Pacific (Singapore) |
| **Amazon EventBridge** | $0-1 | Route events | Asia Pacific (Singapore) |
| **Step Functions** | $0-1 | Orchestrates the workflow | Asia Pacific (Singapore) |
| **S3** | $1.07-2 | Stores forensic evidence | Asia Pacific (Singapore) |
| **Athena** | $0.29-1 | SQL queries against forensic data | Asia Pacific (Singapore) |
| **GuardDuty** | $1.80-2 | Detects security findings | Asia Pacific (Singapore) |
| **CloudTrail** | $0.55-1 | Logs all actions | Asia Pacific (Singapore) |
| **CloudWatch** | $0-1 | Monitoring and dashboards | Asia Pacific (Singapore) |
| **SNS** | $0-1 | Incident notifications | Asia Pacific (Singapore) |
| **API Gateway** | $0.05-1 | Dashboard backend API | Asia Pacific (Singapore) |
| **Cognito** | $0-1 | Dashboard authentication | Asia Pacific (Singapore) |
| **CloudFront** | $0-1 | Dashboard CDN acceleration | Asia Pacific (Singapore) |
| **EC2 (t3.micro)** | $0-1 | Optional analysis instances | Asia Pacific (Singapore) |
| **KMS** | $1.12-2 | Key management | Asia Pacific (Singapore) |
| **Firehose** | $0.04-1 | Deliver data | Asia Pacific (Singapore) |
| **Total** | **$5.01-19** | | |

**Key Assumptions:**

For our setup, it cost around **$5.01** for the whole month with this usage:

* Typical usage: 20-150 incidents per month
* Dashboard served through CloudFront with WAF
* Athena queries optimized with partitioning

**I added $1 to every services to scale with BIGGER INFRASTRUCTURES.**

---

## 5. Team

**AWS FCJ Program Lead (Mentor)**

* **Name:** Nguyễn Gia Hưng
* **Title:** Head of Solutions Architect
* **Description:** Provides technical mentorship, architecture review, and AWS best practices guidance.
* **Email:** hunggia@amazon.com

**Project Stakeholders**
* **Team:** AWS FCJ Mentors.
* **Title:** Program Instructor
* **Stakeholder for:** Academic oversight, project evaluation, internship credit

**Internship Team (FPT University)**

| Name | Title | Role | Email |
| :--- | :--- | :--- | :--- |
| **Huỳnh An Khương** | Team Lead | Coordination, Architecture design, CDK, GuardDuty, Lambda, ETL Pipeline, Forensic analysis. | huynhankhuong0511@gmail.com |
| **Mai Quốc Anh** | Member | Project Management (Jira), Alerting (Email/Telegram), Authentication, Dashboard design. | maiquocanh2608@gmail.com |
| **Nguyễn Trần Minh Quân** | Member | Lambda, ETL Pipeline, Forensic analysis, Alerting (Slack). | nguyentranminhquanb@gmail.com |
| **Lâm Gia Kiệt** | Member | Dashboard design/deployment, CDK, CloudFront, API Gateway. | lamgiakiet2005@gmail.com |
| **Lê Trần Gia Huy** | Member | Lambda, Step Functions automation development, GuardDuty, Eventbridge, Policies and IAM roles. | huyletran188205@gmail.com |

**Project Escalation Contact**

* **Name:** Huỳnh An Khương
* **Title:** Team Lead
* **Role:** Primary contact for project status and escalations
* **Email:** huynhankhuong0511@gmail.com

---

## 6. Resources & Cost Estimates

**Resource Breakdown**

| Resource | Responsibility |
| :--- | :--- |
| **Huỳnh An Khương** | Coordination, Architecture design, CDK, GuardDuty, Lambda, ETL Pipeline, Forensic analysis |
| **Mai Quốc Anh** | Project Management (Jira), Alerting (Email/Telegram), Authentication, Dashboard design, Proposal. |
| **Lâm Gia Kiệt** | Dashboard development, CDK, CloudFront, API Gateway, Gitlab workflow |
| **Nguyễn Trần Minh Quân** | Lambda, ETL Pipeline, Forensic analysis, Alerting (Slack), Validation, Documentation |
| **Lê Trần Gia Huy** | Lambda, Step Functions automation development, GuardDuty, Eventbridge, Policies and IAM roles. |

The cost was too low for us to actually account for the Rate(USD)/Hour cost.

**Hours by Project Phase**

| Project Phase | Huỳnh An Khương | Mai Quốc Anh | Lâm Gia Kiệt | Nguyễn Trần Minh Quân | Lê Trần Gia Huy | Total Hours |
| ---: | :---: | :---: | :---: | :---: | :---: | :---: |
| *Foundation* | 30 | 30 | 30 | 30 | 30 | 150 |
| *Core Orchestration* | 30 | 30 | 30 | 30 | 30 | 150 |
| *Analytics Layer* | 30 | 30 | 30 | 30 | 30 | 150 |
| *Testing & Validation* | 30 | 30 | 30 | 30 | 30 | 150 |
| *Documentation & Handover* | 30 | 30 | 30 | 30 | 30 | 150 |
| **Total Hours** | **150** | **150** | **150** | **150** | **150** | **750** |

It’s not easy to get the exact time we spent on the project, though we average 5 hours per day on it, so I’ll write 5 for every single day.

**Cost Distribution**

| Party | Contribution (USD) | % of Total |
| ---: | :--- | :---: |
| *AWS FCJ Program* | $0 (Non-profit internship) | 0% (academic credit) |
| *FPT University* | Student labor (internship) | 0% (academic credit) |
| *AWS* | $15 (Including running for testing.) | 100% |
| **Total Project Cost** | **$15** | **100%** |

This is cost-effective because team members are completing this as their internship (counting toward academic requirements), and AWS covers infrastructure costs through the FCJ program.

## 7. Acceptance

### Phase Acceptance Criteria

Upon completion of each phase, the team submits deliverables to the AWS FCJ Program Lead and project stakeholders. Within 5 business days, reviewers evaluate deliverables against acceptance criteria. If approved, the phase is accepted. If issues exist, the team receives specific feedback and has 5 business days to address and resubmit.

**Phase 1 Acceptance:** Architecture document reviewed and approved, all team members complete AWS training, GitHub repository set up and working with proper documentation.

**Phase 2 Acceptance:** Step Functions workflow runs end-to-end without crashing, Lambda functions tested and working, EventBridge integration functioning, SNS notifications triggering correctly, integration tests, code has no critical security issues.

**Phase 3 Acceptance:** S3 storage operational with proper partitioning, Athena tables queryable, ETL process normalizing data correctly, documentation complete with 15+ query examples.

**Phase 4 Acceptance:** Dashboard loads without errors, API Gateway connecting to backend, CloudFront CDN serving content, query results displaying in real-time, user-friendly interface tested.

**Phase 5 Acceptance:** Cognito authentication working, simulated incident workflows execute correctly from start to finish, performance benchmarks meet targets (incidents processed within 60 seconds).

**Phase 6 Acceptance:** Deployment guide is clear enough that someone new to the project can follow it and set up the system, GitHub repository is public with comprehensive README, live demonstration runs without major issues, team retrospective documents lessons learned.

### Project Success Evaluation

The project is considered successful if:

* All phases are accepted on time or within 1 week of deadline
* Team members can demonstrate understanding of AWS services used (GuardDuty, Step Functions, Data Firehose, Athena, Cognito, etc.)
* GitHub repository is public and includes complete documentation
* Live workshop demonstration successfully shows incident response in action from detection to dashboard analysis.
* Deployment guide enables a new team to set up the system independently within 1 hour.
* AWS costs stay within the estimated $5/month for typical usage
* End-to-end incident response completes within 60 seconds.

---

## Appendices

### Appendix A: Technology Stack

**Frontend & Dashboards:**
* Custom HTML/CSS/JavaScript
* AWS Management Console

**Backend & Processing:**
* AWS Step Functions (workflow orchestration)
* AWS Lambda (Python 3.12)
* Amazon EC2 (analysis instances)

**Data & Storage:**
* Amazon S3 (forensic evidence storage)
* Amazon EBS (snapshots)
* Amazon Athena (SQL queries against S3 data)
* AWS CloudTrail (audit logs)
* AWS CloudWatch (flow logs)

**Infrastructure & Automation:**
* AWS CDK (Infrastructure-as-Code, Python)
* GitHub (version control and CI/CD)
* GitLab (version control and CI/CD)

**Security & Monitoring:**
* Amazon GuardDuty (threat detection)
* Amazon CloudWatch (monitoring and alarms)
* Amazon Cognito (authentication)

### Appendix B: Key Glossary

| Term | Definition |
| :--- | :--- |
| **AWS FCJ** | AWS First Cloud Journey - internship program for students |
| **GuardDuty** | AWS service that automatically detects security threats |
| **Step Functions** | AWS service for orchestrating serverless workflows |
| **Lambda** | AWS serverless compute - run code without managing servers |
| **CDK** | AWS Cloud Development Kit - write infrastructure as code |
| **Forensics** | Collecting and analyzing evidence from security incidents |
| **Chain of Custody** | Complete audit trail showing who touched what evidence when |
| **Incident Response** | Process of responding to security events |
| **IaC** | Infrastructure as Code - defining infrastructure in code |

### Appendix C: References

* AWS Prescriptive Guidance: Automate incident response and forensics ([https://aws.amazon.com/prescriptive-guidance/](https://aws.amazon.com/prescriptive-guidance/))
* AWS Well-Architected Framework ([https://aws.amazon.com/architecture/well-architected/](https://aws.amazon.com/architecture/well-architected/))
* AWS Step Functions Documentation ([https://docs.aws.amazon.com/step-functions/](https://docs.aws.amazon.com/step-functions/))
* AWS Lambda Best Practices ([https://docs.aws.amazon.com/lambda/](https://docs.aws.amazon.com/lambda/))
* AWS CDK Documentation ([https://docs.aws.amazon.com/cdk/](https://docs.aws.amazon.com/cdk/))
* AWS Free Tier Details ([https://aws.amazon.com/free/](https://aws.amazon.com/free/))

---

**Document Version:** 1.0  
**Last Updated:** December 8, 2025  
**Status:** Ready for Review & Approval  
**Project Code:** AWS-FCJ-IR-FORENSICS-2025
