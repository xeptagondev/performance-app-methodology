# Individual Projects


## Data Sources 
Table names in UNDP Data Warehouse: 
| Table name      | Fields                                                                 |
|-----------------|------------------------------------------------------------------------|
| `[UNDP_IATI].[UNDP_PROJECTS]`   | Closed status, Project ID, Modality, Project Title, Implementing Partner, Description, Project Manager Name, Project Manager Email |
|  `[UNDP_IATI].[UNDP_MARKERS]`    | Project Markers                                                       |
|  `[UNDP_IATI].[IATI_FINANCIALS]` | Funding Partners                                                      |
| `[SF_UNITY].[Opportunity]` | Funded Amount |
| `[PPM_Ext].[XXPROJ_GMS_PROJECT_DETAILS]` | GMS Rate |
| `[UNDP_IATI].[UNDP_INDICATORS]` | Result Based Work plan Data |




## Overview

- **Closed status:** Open, Operationally Closed, Financial Closed. 
- **Project ID:**  01001220
- **Modality:**  NIM (National Implementation Modality), DIM (Direct Implementation Modality). 
- **Project Title:**  The title of the project.
- **Project Markers:**  Innovation, Partners, Digital, HOWS, OECD, Climate, Human Rights, WHOS, Gender, Sustaining Peace.
- **Implementing Partner:**  The implementing partner is the entity that is responsible for the implementation of the project.
- **Responsible Party:**  This is where you have an implement agent that is not UNDP and not the implementing partner. 
- **Description:**  A description of the project. 
- **Project Manager Photo**: The photo of the project manager pulled from IDM
- **Project Manager Name:** The name of the project manager (is always UNDP, regardless of the implementing partner as we place a responsible UNDP person)
- **Project Manager Email:** UNDP email of the project manger.

**Funding Partners**  
|        | Name                                   | Amount   |
|--------|----------------------------------------|----------|
| ![DFAT](image) | Australian DFAT                        | $3.15M   |
| ![UNDP](image) | UNITED NATIONS DEVELOPMENT PROGRAMME   | $-0.04K  |


## Funding Details 
- **Total Budget** - The sum of expense up to current year and budget of current year
- **Funded** – Funded amount by signed agreements
- **Unfunded** - ( Total budget - Funded )
- **Contribution Received** - Amount of Tranches received 
- **Contribution Pending** - ( Sum of Signed Agreements for the project - Contributions )
- **Total Delivery** – Sum of the monetary amount of delivery (2018- Current year)
- **Total Current year Budget** - Current year budget amount
- **Total Current Year Delivery** - Current year delivery monetary amount
- **GMS Rate** - GMS rate 



## Project Library



## Project Alerts



- **PQA**:  Simple check if it done or not based on PQA database in the last two calendar years based on today's date. 
- **SESP**: Simple check if it done or not based on SESP database.
- **Delivery**: Is delivery lagging behind based on linear analysis vs project timeline. Using the global linear average. 
- **Contributions**: If any payment tranches are overdue we can put an alert on that. Open question: how to handle multiple tranches that are overdue. 
- **Project Document not uploaded**: If we cannot find a documented categorized as a project document in the project document library, we will flag this here.
- **Missing Project Board Meeting Minutes**: If we cannot find a project board meeting minutes in the project documentlibrary, we will flag this here. (This has a dependency on ITM)
- **Missing Results**: If there are missing results for any output for previous years, we will flag this here.
- **Evaluation**: If there are overdue management actions, we will flag this here.
- **SECU Case**: If there is an open SECU case, we will flag this here,  link to the registry page. 
- **SRM Case**: If there is an open SRM case, we will flag this here, perhaps link to the registry page. 
- **No Cost Extension**: If there is no cost extension, we will flag this here. Show original close date and extension date
- **Approaching/Overdue Financial Closure**: If the project is approaching or overdue for financial closure, we will flag this here. Counting from the date of the operational closure.
- **Missing LPAC**: If there is no LPAC in the project document library, we will flag this here.
- **Audit & HACT**: This would show upcoming audits, but we need to discuss with OAI if we can get this data. 



## Programme & Project Management (PPM)

## Results Based Workplan

- **Task Number** -  Output 1,2...
- **Task Name** - Name of the task
- **Total Budget**  -  Total budget allocated for the task
- **Activities** - List of indicators and their completion details
- **Indicator Code** - 1.1, 1.2 ,...
- **Indicator description** - Small description about the activity
- **Completion Details** - The actual result value over the target value
- **Result** - The average of the completions of activities under the task
- **Delivery** - Total expenditure of the task over budget 

## Funding Profile

### Overview 

### Funding Partners

- **Allocated** - Total budget calculated same as previously
- **Paid** -  Total expenditure
- **Remaining** - ( Total budget - Total expenditure )

### Payment Tranches

- **FundingPartnerName**: The name of the funding partner.
- **Amount**: The amount of the payment.
- **Date**: The date of the payment.
- **Status**: The status of the payment.

### Risk Register

- **Events**: A brief description of the risk event or scenario that could affect the project (e.g., "Political instability affects project implementation").
- **Impact Level**: A numerical rating (e.g., 1–5) indicating the potential severity of the risk's consequences if it occurs.
- **Likelihood**: A numerical rating (e.g., 1–5) representing the probability of the risk event happening.
- **Risk Level**: The overall risk rating (e.g., Low, Medium, High), typically derived from the combination of Impact Level and Likelihood.
- **Category**: The type or domain of the risk (e.g., Political, Financial, Security, Technical, Environmental, Operational).
- **Causes**: The underlying factors or triggers that could lead to the risk event (e.g., "Election cycles and policy changes").
- **Impacts**: The specific effects or consequences on the project if the risk materializes (e.g., "Project delays and budget overruns").
- **Activities for Treatment**: The mitigation measures or actions planned to reduce the likelihood or impact of the risk (e.g., "Engage stakeholders early and maintain political neutrality. Develop contingency plans for policy transitions.").