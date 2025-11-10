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
| `[UNDP_IATI].[UNDP_INDICATORS]` | Result Based Workplan Data |


The same datasets from `[UNDP_IATI].[UNDP_PROJECTS]` and `[UNDP_IATI].[IATI_FINANCIALS]` that are used to calculate the Master Project List are also applied here.

### Columns Used For Generating Aggregated Data Files
<details>

<summary>Columns in IATI_FINANCIALS data</summary>

* **PROJECT\_NUMBER:** Number assigned to the project.
* **TASK\_ID:** Identifier for the task.
* **TASK\_NUMBER:** Number assigned to the task.
* **FUND\_CATEGORY:** Category that the funding falls into.
* **DONOR:** Code representing the donor.
* **DONOR\_DESCR:** Full name of the donor.
* **fiscal\_year:** Fiscal year range (2023 to 2031).
* **Budget:** Project budget amount in USD.
* **Expenditure:** Total amount of money expended (includes negative numbers).

</details>
<details>

<summary>Columns in UNDP_PROJECTS data </summary>

* **PROJECT\_NUMBER:** Number assigned to the project.
* **PROJECT\_NAME:** Name of the project.
* **PROJECT\_DESCRIPTION:** Description of the project.
* **START\_DATE:** Start date of the project.
* **CLOSED\_DATE:** Date when the project was closed.
* **PROJECT\_TYPE:** Type of project.
* **PROJECT\_STATUS:** Status of the project.
* **PROJECT\_MANAGER:** Project manager's name.
* **PROJECT\_MANAGER\_EMAIL:** Email address of the project manager.
* **IMPLEMENTING\_PARTNER:** Implementing partner code.
* **IMPLEMENTING\_PARTNER\_DESCRIPTION:** Description of the implementing partner.
* **IMPLEMENTATION\_MODALITY:** Implementation modality code.

</details>
<details>

<summary>Columns in UNDP_MARKERS data</summary>

* **PROJECT_NUMBER** - Number assigned to the project.
* **marker_type** - HOWS, WHOS, OECD, Partners, Gender, Digital, Sustaining Peace, Climate, Humanitarian, SSC, COVID, Joint Programme, Innovation, Human Rights

</details>
<details>
<summary>Columns in SF_UNITY.Opportunity  data</summary>

* **Project_ID__c,** - Identifier for the project.
* **StageName** - The stage of the opportunity - Agreement Signed / Engagement Achieved, Agreement Signed (100%), A-Hard Pipeline (90%), B-Soft Pipe Line (50-70%), C- Ideas (30%), C- Ideas (10%) - (**Here we consider only Agreement Signed**).
* **Total_Target_Funding__c** - Target of the funding expected from the opportunity. 

</details>
<details>
<summary>Columns in XXPROJ_GMS_PROJECT_DETAILS data</summary>

* **PROJECT_NUMBER** - Number assigned to the project.
* **GMS_RATE** - GMS rate

</details>
<details>
<summary>Columns in UNDP_INDICATORS data</summary>

* **PROJECT_NUMBER** - Number assigned to the project.
* **TASK_NUMBER** - Output number ( Output 1, Output 2, ...)
* **TASK_NAME** - Name of the output
* **INDICATOR_ID** - Identifier of the activities under the output
* **INDICATOR_CODE** - Numeric code of the activity ( 1.1 , 1.2, ..)
* **INDICATOR_DESCRIPTION** - Description of the activity
* **VALUE_TYPE** - Value type as Number, Percentage, Text, Rating, Boolean
* **TARGET_VALUE** - Target value of the activity
* **ACTUAL_VALUE** - Result value of the activity

</details>

### Other Data Sources 

- **DataCube** - Delivery and Contribution data.
- **atlas_fin_donors_20250806.xlsx** - Old financial data (2012 - 2022).


## Data Aggregation 

Using the above sources, two separate dta files will be created as `Project Data` and `Activity Data`.

### Project Data File

- Load the data from  `[UNDP_IATI].[IATI_FINANCIALS]` ,  `[UNDP_IATI].[UNDP_PROJECTS]`  , `[UNDP_IATI].[UNDP_MARKERS]` , `[PPM_Ext].[XXPROJ_GMS_PROJECT_DETAILS]` and `atlas_fin_donors_20250806.xlsx` .
-  From  `[UNDP_IATI].[IATI_FINANCIALS]` we consider only the recodes were `FUND_CATEGORY` is `PROGRAMME`.

```
# Filter financials for PROGRAMME category
financials_df = financials_df[financials_df['FUND_CATEGORY'] == 'PROGRAMME']
```
- When calculating the budget, we apply a customized logic: if the fiscal year is greater than or equal to the current year, we use 'Budget'; otherwise, we use 'Expenditure'.
```
def calculate_budget(row):
   # If fiscal_year is greater than or equal to the current year, use 'Budget', otherwise use 'Expenditure'
   if row['fiscal_year'] >= current_year:
      return row['Budget']
   else:
      return row['Expenditure']
```
- Project markers data will be taken as a list of unique values per `PROJECT_NUMBER`.
```
# Merge markers data
grouped_markers = markers_df.groupby(['PROJECT_NUMBER']).agg(
   markers =('marker_type', lambda x: ', '.join(x.unique()))
).reset_index()
```
- GMS rate is calculate as the average of ono-zero values for a `PROJECT_NUMBER`.
```
# Group GMS details by PROJECT_NUMBER and calculate the mean GMS_RATE, ignoring zeros
def mean_ignore_zeros(series):
   non_zero = series[series != 0]
   return non_zero.mean() if not non_zero.empty else 0

grouped_gms_details = gms_details_df.groupby('PROJECT_NUMBER').agg(
   gms_details=('GMS_RATE', mean_ignore_zeros)
).reset_index()
```

- Then all the data will be `LEFT` join to the filtered `IATI_FINANCIALS` data on `PROJECT_NUMBER`.

### Activity Data

- Load the data from  `[UNDP_IATI].[IATI_FINANCIALS]` and `[UNDP_IATI].[UNDP_INDICATORS]`.
- Then do the same filtering for  `[UNDP_IATI].[IATI_FINANCIALS]` and apply the budget calculation .
- Group the indicator data by `PROJECT_NUMBER, TASK_NUMBER, and INDICATOR_ID`, and calculate the average target and result values for each activity.
```
# Use groupby with aggregation dictionary for performance
grouped_indicator = indicator_df.groupby(['PROJECT_NUMBER', 'TASK_NUMBER', 'INDICATOR_ID'], sort=False).agg({
   'TASK_NAME': 'first',
   'PROJECT_NUMBER': 'first',
   'TASK_NUMBER': 'first',
   'INDICATOR_DESCRIPTION': 'first',
   'TARGET_VALUE': 'mean',
   'ACTUAL_VALUE': 'mean',
   'INDICATOR_CODE': 'first'
}).reset_index()
```
- Calculate the completion percentage for each activity as `Actual / Target`, ensuring the result is constrained between 0% and 100%.
- To further reduce file size and simplify calculations, group the data by `PROJECT_NUMBER` and `TASK_NUMBER`. The task-level completion percentage should be calculated as the mean of the activity-level completion percentages.
- Then, the financial data will be left-joined with this dataset.


### Opportunity Data for Funded Amount
- To calculate the funded amount per project, take the sum of `Total_Target_Funding__c` for records where StageName begins with _"Agreement Signed"_.
```
funded_amount = project_data.loc[project_data['StageName'].str.startswith('Agreement Signed'), 'Total_Target_Funding__c'].sum()

```




## Overview

- **Closed status:** Open, Operationally Closed, Financial Closed. 
- **Project ID:**  Number assigned to the project (01001220)
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

Each alert card uses a traffic light color system to indicate status.

| Alert Name | Description | 🔴 Red | 🟡 Yellow | 🟢 Green | Display Notes |
|------------|-------------|--------|-----------|----------|---------------|
| **PQA** | Check if PQA is done based on PQA database in the last two calendar years | PQA is missing | - | PQA is complete | Always show |
| **SESP** | Check if SESP is done based on SESP database | SESP is missing | - | SESP is complete | Always show |
| **Delivery** | Delivery performance based on linear trendline analysis vs project timeline | Score <70% | Score 70-84% | Score 85%+ | Always show |
| **Project Document** | Check if project document exists in the project document library | Cannot find project document | - | Project document found | Always show |
| **Project Board Meeting Minutes** | Check if project board meeting minutes exist in project document library | Cannot find meeting minutes | - | Meeting minutes found | Always show (ITM dependency) |
| **Missing Results** | Check if there are missing results for any output for previous years | Missing results detected | - | All results present | Always show |
| **Overdue Management Actions** | Check if there are overdue management actions from evaluations | Overdue actions exist | - | No overdue actions | Always show |
| **SEQ Case** | Check if there is an open SEQ case (link to registry page) | Open SEQ case exists | - | - | Only show if open case exists |
| **SRM Case** | Check if there is an open SRM case (link to registry page) | Open SRM case exists | - | - | Only show if open case exists |
| **No Cost Extension** | Check if there is a no cost extension (show original close date and extension date) | - | Extension exists | - | Only show if extension exists |
| **Financial Closure** | Check if project is approaching or overdue for financial closure (counting from operational closure date) | Overdue for closure | Approaching closure | On track | Always show |
| **LPAC** | Check if LPAC exists in the project document library | LPAC is missing | - | LPAC found | Always show |
| **Audit & HACT** | Show upcoming audits | TBD | TBD | TBD | Pending OAI data discussion |
| **Contributions** | Check if any payment tranches are overdue | TBD | TBD | TBD | Open question: how to handle multiple overdue tranches | 



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