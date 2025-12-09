---
title: "Week 9 Worklog"
date: "2025-09-09"
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---
### Week 9 Objectives:

* Keep working on the workshop

### Tasks to be carried out this week:


| Day | Task                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Start Date | Completion Date | Reference Material                                                                       |
| ----- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | ----------------- | ------------------------------------------------------------------------------------------ |
| 2   | - AWS Architecture revised:<br>&emsp; + Removed AWS Detective <br>&emsp; + Updated with Step Function Workflow instead of a singular AWS Lambda Function <br>&emsp; + Added Custom Dashboard: A static custom dashboard website hosted with S3 and use Athena to query from data lake <br>                                                                                                                                                                                              | 03/11/2025 | 03/11/2025      |                                                                                          |
| 3   | - Start on writing and reviewing inline poilicies for Lambdas and User Roles.                                                                                                                                                                                                                                                                                                                                                                                                           | 04/11/2025 | 04/11/2025      |                                                                                          |
| 4   | - Team meetings: Progress report:<br>&emsp; + IR Workflow: Halfway done, EC2 quarantine function is finished, not tested with findings yet.                                                                                                                                                                                                                                                                                                                                             | 05/11/2025 | 05/11/2025      |                                                                                          |
| 5   | - Team meetings<br> - Researched on ETL Pipeline approach: <br>&emsp; + Instead of using Glue ELT Jobs, we use custom Lambda ELT pipeline for CloudTrail and CloudWatch  logs <br>&emsp; + Store raw logs into a Raw Log S3 Bucket then use ETL Lambda to process the data and write it to a Proccesed Data S3 to then be Crawled <br> - AWS Architecture revised: Added a new group: DATA PREP group which contain the Raw Log S3 Bucket and the ETL Lambda <br>- School subject: <br> | 06/11/2025 | 06/11/2025      | [Advanced Writing](https://www.coursera.org/account/accomplishments/verify/EDQ1NY2UG063) |
| 6   | - Researched on Kinesis Data Firehose to collect log: Good for future usage, not suitable for current project because real time streaming data was not necessary, using batch processing is better<br> - Succesfully build an ETL Pipeline for CloudTrail logs: Triggered by object creation in CloudTrail Raw Log Bucket and reformatted the raw logs into JSONL and save it into Proccessed S3 <br> - Succesfully crawled and queried the processed log to show CloudTrail Events     | 07/11/2025 | 07/11/2025      |                                                                                          |

### Week 9 Achievements:

* **Architecture Refinement & Decision Making:**
    * Updated the Incident Response (IR) mechanism to use a **Step Functions Workflow** instead of a single Lambda function to improve orchestration.
    * Introduced a **Custom Dashboard** strategy (static website hosted on S3) that uses Athena to query the data lake.
    * Conducted a comparative analysis between **AWS Kinesis Data Firehose** and batch processing; selected the batch approach for cost-efficiency as real-time streaming was not required.

* **Data Pipeline Implementation:**
    * Created a new **DATA PREP** architectural group, featuring a Raw Log S3 Bucket and a custom ETL Lambda.
    * Built and deployed a **serverless ETL Lambda pipeline** to process CloudTrail logs, automatically triggered by new object creation in the Raw Log S3 Bucket.
    * Successfully crawled and queried the processed CloudTrail logs (formatted as JSONL) using **AWS Glue and Athena**.
    

* **Security & IAM Configuration:**
    * Started the security hardening process by writing and reviewing **inline policies** for Lambda functions and User Roles to ensure least-privilege access.

* **Project Progress:**
    * Achieved 50% completion of the IR Step Functions Workflow, with the **EC2 quarantine function** fully coded (pending findings test).
