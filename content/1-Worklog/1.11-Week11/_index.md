---
title: "Week 11 Worklog"
date: "2025-11-17"
weight: 2
chapter: false
pre: " <b> 1.11. </b> "
---
### Week 11 Objectives:

* Optimize architecture for cost and reliability (SQS integration & S3 API analysis).
* Deepen knowledge of Edge Security (WAF/CloudFront) and Infrastructure as Code (CDK).
* Finalize EC2 isolation testing and refine the custom dashboard.

### Tasks to be carried out this week:


| Day | Task                                                                                                                                                                                                                                                                                        | Start Date | Completion Date | Reference Material                                                                                                               |
| :---: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----------: | :---------------: | :--------------------------------------------------------------------------------------------------------------------------------- |
|  2  | - Joined the**AWS Cloud Mastery Series #2**: Gained insights on CDK and CloudFormation for the project and received mentor recommendations on demo strategy.<br> - Wrote a recap of the event experience.                                                                                   | 17/11/2025 |   17/11/2025   |                                                                                                                                  |
|  3  | -Initiated a pricing update plan.<br> - **Implementation:**<br>&emsp; + Successfully isolated EC2 in the testing environment.<br>&emsp; + Upgraded CloudWatch ETL Lambda to process logs via triggers without Crawlers.<br> - Backed up all Lambda function codes.                          | 18/11/2025 |   18/11/2025   |                                                                                                                                  |
|  4  | - Joined the**Secure Your Applications: AWS Perimeter Protection Workshop**.<br>&emsp; + Deep dived into CloudFront and WAF configuration.<br>&emsp; + Reviewed the new CloudFront pricing tier.<br> - Learnt how to set up **API Gateway REST APIs** to prepare for dashboard integration. | 19/11/2025 |   19/11/2025   | [AWS Perimeter Protection](https://catalog.us-east-1.prod.workshops.aws/workshops/32e6bc9a-5c03-416d-be50-34358a8a5f64/en-US)    |
|  6  | - Researched **AWS CDK**: Installation, usage, and stack configuration to prepare for next week's migration to IaC.                                                                                                                                                                         | 21/11/2025 |   21/11/2025   | [AWS CDK Github](https://github.com/aws/aws-cdk) <br><br> [AWS CDK Document](https://docs.aws.amazon.com/cdk/v2/guide/home.html) |

### Week 11 Achievements:

* **Architecture Optimization & Cost Management:**

  * Refined the event-driven architecture by decoupling EventBridge and Step Functions using **Amazon SQS** to ensure message durability and reliability.
  * Formulated a plan to optimize API costs.
  * **Security & Network Learning:**
* * Gained practical experience in perimeter protection by completing the **AWS Perimeter Protection Workshop**, focusing on **AWS WAF** (Web Application Firewall) and **Amazon CloudFront** configurations.
* Researched **API Gateway REST APIs** to facilitate the future integration of the custom security dashboard.
* **Infrastructure as Code (IaC) Preparation:**

  * Leveraged insights from the **AWS Cloud Mastery Series #2** to plan the project's migration to Infrastructure as Code.
  * Completed foundational research on **AWS CDK**, covering installation, stack configuration, and construct usage to prepare for the implementation phase.
* **Project Implementation:**

  * Successfully executed and verified **EC2 Isolation** logic in the live testing environment.
  * Updated the custom dashboard frontend to display more relevant security fields.
