# Project Quality Assurance

For historical reasons, the SESP and PQA Data are stored together.

Downloading the data from the UNDP Data Warehouse, provides a CSV file with the following columns:

* **OperatingUnit**: Identifies the operational unit associated with the project, indicating the specific geographic or organizational division.
* **Bureau**: Specifies the bureau within the organization that oversees the project, representing a higher-level administrative grouping.
* **isActive**: A binary indicator (1 for active, 0 for inactive) showing whether the project is active in the year. 
* **Year**: The year associated with the project's data entry, indicating when the project was either initiated or recorded in the system.
* **isQA\_Eligible**: A binary flag (1 for yes, 0 for no) denoting whether the project is eligible for Quality Assurance (QA) processes.
* **isQA\_Required**: Another binary flag (1 for yes, 0 for no) indicating whether the project requires QA based on specific criteria or standards.
* **QA\_Status**: Describes the QA status of the project, such as "Exempted" or "Completed," detailing the outcome of the QA process.
* **isSESP\_Required**: A binary indicator (1 for yes, 0 for no) showing whether the project requires Social and Environmental Standards Screening Procedures (SESP).
* **SESP\_Status**: Reflects the current status of the SESP process for the project, with possible values like "Not Monitored," "Pending," or "Completed."
* **ProjectNum\_Unified**: A unique identifier for each project, allowing for consistent tracking and referencing across different records or databases.
* **ApprovedDate**: The date and time when the project received approval, formatted as a timestamp, indicating when the project was officially sanctioned.
* **Project Current Status**: Indicates the current status of the project, used to determine whether a project is active as of today. Possible values include:
  * Financially Closed
  * On Going
  * Operationally Closed
  * Submit for Operational Close
  * Submitted for Financial close

## Definition of "Closed"

A project is defined as "Closed" based on the earliest change of project status to “Operationally Closed”, “Submitted for Financial close” or “Financially Closed”. 

Note: if Project Status goes back to “On Going” for more than 90 days, earliest closure is ignored, and we consider this project "Ongoing". 


## PQA Statuses

1. **Exempted**
2. **Completed**
3. **Not Required**
4. **Not Started**
5. **In Progress**

### Project Types

Some project types are exempt from PQA. Here is the full list of project types in the Data Warehouse and whether they are eligible or exempt from PQA. 

| Code  | Atlas Project Type                   | Current Project Type               | Eligibility |
|-------|--------------------------------------|-------------------------------------|-------------------|
| CNT   | Country Development Project          | Development Project                 | Eligible          |
| DEVEF | Development Effectiveness            | Development Effectiveness Project   | Exempt            |
| DEVT  | Development Project Proposal         | Project Initiation Plan             | Exempt            |
| DSERV | Development Service                  | Development Services Project        | Exempt            |
| ENGMT | Engagement Facility                  | Engagement Facility                 | Exempt            |
| FCORE | Fully Funded by Core Resources       | Development Project                 | Eligible          |
| FNONC | Fully Funded by Single Donor         | Development Project                 | Eligible          |
| FPART | Partially Funded (Multi Donor)       | Development Project                 | Eligible          |
| GLO   | Global Project                       | Development Project                 | Eligible          |
| INT   | Initiation Plan                      | Project Initiation Plan             | Exempt            |
| MGMT  | Management Project                   | Management Project                  | Exempt            |
| MSA   | Management Service Agreement         | Development Services Project        | Exempt            |
| PROJM | Program Management                   | Program Management Project          | Exempt            |
| RAF   | Regional Project Africa              | Development Project                 | Eligible          |
| RAP   | Regional Project Asia Pacific        | Development Project                 | Eligible          |
| RAS   | Regional Project Arab States         | Development Project                 | Eligible          |
| REC   | Regional Project Europe & CIS        | Development Project                 | Eligible          |
| RLA   | Regional Project LAC                 | Development Project                 | Eligible          |
| RMCOR | Core Regular                         | Development Project                 | Exempt            |
| RMFLC | Fully Funded by Local Cost           | Development Project                 | Exempt            |
| RMPLC | Partially Funded by Local Cost       | Development Project                 | Exempt            |
| SSC   | Multi Country Project/SSC Proj       | Development Project                 | Eligible          |
| UNC   | UN Coordination                      | Management Project                  | Exempt            |
| UNV   | United Nations Volunteers            | Management Project                  | Exempt            |


## Calculation Methodology

1. **Filtering by Bureau**: Initially, we select projects that are part of specific bureaus, namely "RBA," "RBAP," "RBAS," "RBLAC," "CB," "BPPS," and "RBEC."
2. **Further Filtering for QA Eligible and Project Status**: Among the projects filtered by bureau, we apply additional criteria to focus on those that:
   * Are marked as requiring QA (`isQA_Eligible` == 1), indicating that they must undergo Quality Assurance processes based on predefined standards or conditions.
   * Are currently active (`Project Status` == "Ongoing") OR
   * Has been closed within the last two years (to the day) based on the definition of "Closed".
3. **Identifying Unique Projects**: After applying these filters, we count the number of unique projects by their `ProjectNum_Unified` identifier. This final step provides the total count of distinct projects meeting all the specified criteria.
4. **Define Complete and Incomplete:**
   A project is considered compliant if it met any of the following:
      * We considered a PQA as "Complete" if the QA Status is `Complete`and ApprovedDate within the last two years as of today's date. OR
      * The project status is “Operationally Completed” or “Financially Completed” and QA Status is `Complete`. OR
      * The project was exempted

5. **Calculating QA Completion Rate:** To calculate the completion rate, we need to determine the total number of projects and the proportion of completed projects. The completion rate is  expressed as a percentage and can be calculated using the following formula: 

Completion Rate (%) = (Total distinct count of PQA Compliant Projects) / (Total distinct count of Ongoing Projects + Closed Project within 2 Years)* 100

To simplify:

Completion rate (%) = (Total Completed PQA / Total Considered Projects)*100


## Resources

- [PQA Policy](https://popp.undp.org/policy-page/quality-standards-programming)
