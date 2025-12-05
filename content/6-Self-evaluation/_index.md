---
title: "Self-Evaluations"
date: 2025-09-10
weight: 6
chapter: false
pre: " <b> 6. </b> "
---



During the internship at **Amazon Web Services** from **9/2025** to **12/2025**, I had the opportunity to learn, practice, and apply the knowledge acquired at school in a real working environment.
I participated in **Autonomous Incident Response Development** with tasks involving EventBridge (Trigger), AWS Lambda Functions, and AWS Step Functions (Core Logic).
### Summary Report of Skills & Implemented Items

During the project implementation process, I performed the following items:

1.  **Orchestration with AWS Step Functions:**
    * Established direct **AWS SDK** integration (Service Integration) to call EC2 and Auto Scaling APIs, eliminating dependency on intermediate Lambdas.
    * Handled Data Flow between states: used `ResultPath: null` to preserve data and `States.Array` to handle dynamic arrays.
    * Configured complex navigation logic: branching (Choice), looping (Map), and automatic retry mechanisms (Retry).

2.  **Auto Scaling Group (ASG) Operations:**
    * Executed the process of detaching instances from ASG using the parameter `ShouldDecrementDesiredCapacity` to maintain application operations.
    * Handled Capacity Constraints, specifically fixing the MinSize logic error by adding the `UpdateASGConfiguration` step.

3.  **Debugging & Troubleshooting:**
    * Analyzed root causes (Root Cause Analysis) by checking the Input/Output of each Step.
    * Performed Isolation Testing for each logic branch (ASG and Non-ASG) and used mock data (Mock events).
    * Identified and handled logic errors that did not report system errors (Silent Failure) and environmental errors (wrong Region, ID format).

4.  **Security & Permission Management (IAM):**
    * Applied the **Least Privilege** principle: Granted limited permissions via Inline Policy for specific actions (such as DetachInstances, CreateSnapshot).
    * Deployed the technical Incident Response process in sequence: Detect $\rightarrow$ Isolate (Security Group) $\rightarrow$ Protect (Termination Protection) $\rightarrow$ Collect Evidence (Snapshot).

5.  **Automation:**
    * Built an automation system to replace manual operations.
    * Designed workflows ensuring **Idempotency** (allowing multiple re-runs without causing duplicate errors) and flexible handling capabilities for both instances within and outside ASG.

Regarding demeanor, I always strive to complete tasks well, adhere to regulations, and actively exchange with colleagues to improve work efficiency.

To objectively reflect on the internship process, I would like to self-assess based on the criteria below:


| No. | Criteria                              | Description                                                                                      | Good | Fair | Average |
| :-- | :------------------------------------ | :----------------------------------------------------------------------------------------------- | :--: | :--: | :-----: |
| 1   | **Professional knowledge and skills** | Understanding of the industry, applying knowledge to reality, tool usage skills, work quality    |  ✅  |  ☐   |    ☐    |
| 2   | **Learning ability** | Absorbing new knowledge, learning quickly                                                        |  ☐   |  ✅  |    ☐    |
| 3   | **Proactivity** | Self-researching, accepting tasks without waiting for instructions                               |  ☐   |  ✅  |    ☐    |
| 4   | **Sense of responsibility** | Completing work on time, ensuring quality                                                        |  ✅  |  ☐   |    ☐    |
| 5   | **Discipline** | Adhering to schedule, regulations, work processes                                                |  ✅  |  ☐   |    ☐    |
| 6   | **Progressiveness** | Ready to receive feedback and improve oneself                                                    |  ✅  |  ☐   |    ☐    |
| 7   | **Communication** | Presenting ideas, reporting work clearly                                                         |  ✅  |  ☐   |    ☐    |
| 8   | **Teamwork** | Working effectively with colleagues, participating in the team                                   |  ✅  |  ☐   |    ☐    |
| 9   | **Professional conduct** | Respecting colleagues, partners, working environment                                             |  ✅  |  ☐   |    ☐    |
| 10  | **Problem-solving mindset** | Identifying problems, proposing solutions, creativity                                            |  ✅  |  ☐   |    ☐    |
| 11  | **Contribution to project/organization**| Work efficiency, improvement initiatives, recognition from team                                |  ✅  |  ☐   |    ☐    |
| 12  | **Overall** | General assessment of the entire internship process                                              |  ✅  |  ☐   |    ☐    |

### Needs Improvement

* Enhance discipline, strictly adhere to the regulations of the company or any organization.
* Improve problem-solving mindset.
* Learn to communicate better in daily interactions and at work, and in handling situations.