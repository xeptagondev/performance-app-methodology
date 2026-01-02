# Individual Projects


## Data Sources 
Table names in UNDP Data Warehouse: 
| Table name      | Fields                                                                 |
|-----------------|------------------------------------------------------------------------|
| `[UNDP_IATI].[UNDP_PROJECTS]`   | Closed status, Project ID, Modality, Project Title, Implementing Partner, Description, Project Manager Name, Project Manager Email |
|  `[UNDP_IATI].[UNDP_MARKERS]`    | Project Markers                                                       |
|  `[UNDP_IATI].[IATI_FINANCIALS]` | Funding Partners                                                      |
|`[UNDP_IATI].[UNDP_PDC]`| Project Document Library Data|
| `[PPM_Ext].[XXPROJ_GMS_PROJECT_DETAILS]` | GMS Rate |
| `[SF_UNITY].[Opportunity]` | Funded Amount |
| `[UNDP_IATI].[UNDP_INDICATORS]` | Result Based Workplan Data  |
| `[Fusion_FIN_Reports].[UNProjectBudgetBalance] ` | Result Based Workplan Data Activity Budget Details and Responsible Parties Data |
|`[FUSION_AR_FACTS_ALL].[UN_AR_Unbilled_Details_Report],[FUSION_AR_FACTS_ALL].[UN_Generate_AR_Invoices_Report]`| Payment Tranches|
|`[SF_UNITY].[Opportunity],[FUSION_AR_FACTS_ALL].[UN_AR_Unbilled_Details_Report],[FUSION_GL_FACTS_ALL].[Resource_Overview_Tbl]`| Contribution Pending and Received |
|`[PPM_Ext].[XXPROJ_UNDP_PROJECT_RISK]`| Project Risk Data|


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
* **BASELINE_VALUE** - Baseline value
* **TARGET_VALUE** - Target value of the activity
* **ACTUAL_VALUE** - Result value of the activity
* **RESULTS_YEAR** - The result year

</details>

<details>
<summary>Columns in UNDP_PDC data</summary>

* **ProjectNumber** - Unified Number assigned to the project.
* **OutputNumber** - Project Number.
* **DocumentCategory** - Category of the document.
* **Title** - Title of the document.
* **Name** - Name of the document.
* **Path** - URL Path of the document.
* **DocumentType** - Sub Category of the document.

</details>

<details>
<summary>Columns in UNProjectBudgetBalance data</summary>

* **project_id** - Number assigned to the project.
* **output** - Output number ( Output 1, Output 2, ...)
* **output_description** - Description of the output 
* **activity** - Activity number or Name ( Activity 1.1, Activity 1.2, ...)
* **activity_description** - Description of the activity
* **tot_budget** - Total budget for the activity
* **total_exp** - Total expenditure for the activity
* **Budget_Period** - Budget year for the activity
* **responsible_party** - Party responsible for the activity
</details>
<!-- <summary>Columns in UN_AR_Unbilled_Details_Report and UN_Generate_AR_Invoices_Report data</summary> -->
<details>
<summary>Columns in XXPROJ_UNDP_PROJECT_RISK data</summary>

* **RISK_ID** - Risk identifier
* **PROJECT_ID** - Project identifier
* **PROJECT_NUMBER** - Project number
* **PRIMARY_CATEGORY_ID** - Primary category identifier (Numeric)
* **SECONDARY_CATEGORY_ID** - Secondary category identifier
* **EVENTS** - Events related to the risk
* **CAUSES** - Causes related to the risk
* **IMPACTS** - Impacts related to the risk
* **IMPACT_ID** - Impact score (1, 2,... 5)
* **LIKELYHOOD_ID** - Likelihood score (1, 2,... 5)
* **RISK_RATING** - Risk rating
* **RISK_LEVEL** - Risk level

</details>

### Other Data Sources 

- **DataCube** - Delivery and Contribution data.
- **atlas_fin_donors_20250806.xlsx** - Old financial data (2012 - 2022).


## Data Aggregation 

Using the above sources, separate data files will be created based on the sections in the Project Overview Page.
- `Project Data` - Summary of the core project data; including project information, budgets, makers and gms details.
- `Project Budget Balance` - The budget details for Result Based Workplan sections. This contains the output wise budget data.
- `Project Result Data` - The result data for Result Based Workplan section.
- `Payment Tranches` - Payment details
- `Project Risk` - Project risk management details

### 1. Project Data File

- Load the data from  `[UNDP_IATI].[IATI_FINANCIALS]` ,  `[UNDP_IATI].[UNDP_PROJECTS]`  , `[UNDP_IATI].[UNDP_MARKERS]` , `[PPM_Ext].[XXPROJ_GMS_PROJECT_DETAILS]` and `atlas_fin_donors_20250806.xlsx` .
-  From  `[UNDP_IATI].[IATI_FINANCIALS]` we consider only the records where `FUND_CATEGORY` is `PROGRAMME`.

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
- The same logics have been applied for atlas_fin_donors_20250806.csv and since it contain only data from 2012-2022, budgets and expenditures are the same.
```
atlas_fin_donor.rename(columns={'output': 'PROJECT_NUMBER','donor': 'DONOR'}, inplace=True)
atlas_fin_donor['PROJECT_NUMBER'] = pd.to_numeric(atlas_fin_donor['PROJECT_NUMBER'], errors='coerce').astype('Int64')
grouped_atlas = atlas_fin_donor.groupby(['PROJECT_NUMBER', 'fiscal_year', 'DONOR']).agg(
      total_budget=('project_expenditure_combined', 'sum'),
      total_expenditure=('project_expenditure_combined', 'sum')
).reset_index()
```
- Project markers data will be taken as a list of unique values per `PROJECT_NUMBER`.
```
# Merge markers data
grouped_markers = markers_df.groupby(['PROJECT_NUMBER']).agg(
   markers =('marker_type', lambda x: ', '.join(x.unique()))
).reset_index()
```
- GMS rate is calculated as the average of ono-zero values for a `PROJECT_NUMBER`.
```
# Group GMS details by PROJECT_NUMBER and calculate the mean GMS_RATE, ignoring zeros
def mean_ignore_zeros(series):
   non_zero = series[series != 0]
   return non_zero.mean() if not non_zero.empty else 0

grouped_gms_details = gms_details_df.groupby('PROJECT_NUMBER').agg(
   gms_details=('GMS_RATE', mean_ignore_zeros)
).reset_index()
```

- Then all the data will be `LEFT` joined to the filtered `IATI_FINANCIALS` data on `PROJECT_NUMBER`.

### 2. Project Activity Budget Data
- Load the data from `[Fusion_FIN_Reports].[UNProjectBudgetBalance]`.
- First group the dat by `ProjectNumber`,`output`,`activity`,`Budget_Period`,`Account` to get the expenditure item level data.
- Then group the data by `ProjectNumber`, `output`,`Budget_Period` and calculate the output level budget and expenditure.
- Then group the data by `ProjectNumber`, `output`, `activity` and `Budget_Period`, summing up the `tot_budget` and `total_exp` to get the total budget and expenditure for each activity.
- Final join all to single dataframe.
<details>
<summary>Click to expand: Project Activity Budget Processing Code</summary>


```
grouped = budget_balance_df.groupby(['ProjectNumber','output','activity','Budget_Period','Account']).agg({
      'output_description': 'first',
      'activity_description': 'first',
      'responsible_party': 'first',
      'tot_budget': 'sum',
      'total_exp': 'sum'
}).reset_index()

# Group budget data by project_id, output, activity, and Budget_Period
    # Calculate budget completion percentage in activity level
   grouped_activity = grouped.groupby(['ProjectNumber','output','activity','Budget_Period']).agg({
         'tot_budget': 'sum',
         'total_exp': 'sum'
   }).reset_index()
   grouped_activity['completion_percentage'] = np.where(
         grouped_activity['tot_budget'] > 0,
         (grouped_activity['total_exp'] / grouped_activity['tot_budget']) * 100,
         0
   )

# Calculate total budget and expenditure per output and completion percentage
budget_summary = grouped.groupby(['ProjectNumber', 'output','Budget_Period']).agg({
      'tot_budget': 'sum',
      'total_exp': 'sum'
}).reset_index()

budget_summary['completion_percentage'] = np.where(
      budget_summary['tot_budget'] > 0,
      (budget_summary['total_exp'] / budget_summary['tot_budget']) * 100,
      0
)
```
</details>



- Calculate the budget completion percentage for each activity as `total_exp / tot_budget`, ensuring the result is constrained between 0% and 100%.

### 3. Project Result Data

- Load the data from `[UNDP_IATI].[UNDP_INDICATORS]`.
- Group the indicator data by `PROJECT_NUMBER, TASK_NUMBER, INDICATOR_ID, and RESULTS_YEAR` as follows.

```
# Use groupby with aggregation dictionary for performance
grouped_indicator = indicator_df.groupby(['PROJECT_NUMBER', 'TASK_NUMBER', 'INDICATOR_ID','RESULTS_YEAR'], sort=False).agg({
      'TASK_NAME': 'first',
      'PROJECT_NUMBER': 'first',
      'TASK_NUMBER': 'first',
      'INDICATOR_ID': 'first',
      'RESULTS_YEAR': 'first',
      'INDICATOR_DESCRIPTION': 'first',
      'TARGET_VALUE': 'first',
      'ACTUAL_VALUE': 'first',
      'INDICATOR_CODE': 'first',
      'VALUE_TYPE': 'first',
      'BASELINE_VALUE': 'first'
}).reset_index()
```
- Calculate the completion percentage for each activity based on `VALUE_TYPE`, ensuring the result is constrained between 0% and 100%
   - Number, Percentage, and Rating - Actual / Target
   - Boolean - 100 if actual equals to target else 0
   - Text - Nan
<details>
<summary>Click to expand: Project Result Processing Code</summary>

```
# Convert to numeric only for calculation, keeping original non-numeric values intact
target_numeric = pd.to_numeric(grouped_indicator['Target'], errors='coerce')
actual_numeric = pd.to_numeric(grouped_indicator['Actual'], errors='coerce')

# Calculate completion_percentage for 'Number', 'Percentage', and 'Rating' Value_Types
value_types_numeric = ['Number', 'Percentage', 'Rating']
grouped_indicator['completion_percentage'] = np.where(
      grouped_indicator['Value_Type'].isin(value_types_numeric) & 
      pd.notna(target_numeric) & 
      pd.notna(actual_numeric),
      np.where(
         (target_numeric == 0) & (actual_numeric == 0),
         0,
         np.round(
            np.where(
                  target_numeric != 0,
                  (actual_numeric * 100 / target_numeric).clip(lower=0, upper=100),
                  0
            ),
            2
         )
      ),
      np.nan
)

# Calculate completion_percentage for 'Boolean' Value_Type where 100 if actual equals to target else 0
grouped_indicator['completion_percentage'] = np.where(
      (grouped_indicator['Value_Type'] == 'Boolean') & 
      pd.notna(grouped_indicator['Target']) & 
      pd.notna(grouped_indicator['Actual']),
      np.where(
         grouped_indicator['Actual'].str.lower() == grouped_indicator['Target'].str.lower(),
         100,
         0
      ),
      grouped_indicator['completion_percentage']
)
```
</details>

- Then, the financial data will be left-joined with this dataset.

### 4. Payment Tranches 
- Load the data from `[FUSION_AR_FACTS_ALL].[UN_AR_Unbilled_Details_Report]` which contain future tranches and `[FUSION_AR_FACTS_ALL].[UN_Generate_AR_Invoices_Report]` for collected tranches.
- Collect the data as follows:
1. `UN_AR_Unbilled_Details_Report` 
   - USD_AMOUNT :- AMOUNT
   - EVENT_DATE :- DATE
2. `UN_Generate_AR_Invoices_Report`
   - RECEIPT_AMOUNT_USD_EQUIVALENT :-AMOUNT
   - ACCOUNTING_DATE :- DATE

### 5. Project Risk 
- Load data from `[PPM_Ext].[XXPROJ_UNDP_PROJECT_RISK]`.
- Get the required columns.

### 6. Opportunity Data for Funded Amount
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

## Funding Partners 
This section represent the donor wise budget from `IATI_FINANCIALS`. 

**Budget** = The sum of expense up to current year and budget of current year


|        | Name                                   | Amount   |
|--------|----------------------------------------|----------|
| ![DFAT](image) | Australian DFAT                        | $3.15M   |
| ![UNDP](image) | UNITED NATIONS DEVELOPMENT PROGRAMME   | $-0.04K  |


## Funding Details 
- **Total Budget** - The sum of expense up to current year and budget of current year
- **Funded** – Funded amount by signed agreements
- **Unfunded** - ( Total budget - Funded )
- **Contribution Received** - Sum of revenue from Resource_Overview_Tbl where ACCOUNT_NUMBER id 14015
- **Contribution Pending** - From UN_AR_Unbilled_Details_Report table summation of UDS amount except EVENT_TYPE not includes revenue + Unit Government cost sharing from Pipeline data
- **Total Delivery** – Sum of the monetary amount of delivery (2018- Current year)
- **Total Current year Budget** - Current year budget amount
- **Total Current Year Delivery** - Current year delivery monetary amount
- **GMS Rate** - GMS rate 

## Project Progress
- **Timeline** - Timeline of the project taken from stat and end date of the project
- **Results** - The mean percentage of Results Achievement over all years and all output
- **Delivery percentage** =  Total Delivery / Total Budget
- **Contribution percentage** = Total Contribution from data cube data / Total Budget


## Project Document Library

- **Document Categories** - Categories of documents available in the project document library (Project,Portfolio,Proposal,Other).
- **Document Title** - Title of the document or Name of the document.
- **URL Path** - URL Path of the document from Docs-Project site in share point.


## Project Alerts
Each alert card uses a traffic light color system to indicate status.

| Alert Name | Description | 🔴 Red | 🟡 Yellow | 🟢 Green | ⚪ Grey (No Data) |Display Notes |
|------------|-------------|--------|-----------|----------|----------|---------------|
| **PQA** | Check if PQA is done based on PQA database in the last two calendar years | PQA is missing | - | PQA is complete |Show if no data for the project number or isQA_Required false| Always show |
| **SESP** | Check if SESP is done based on SESP database | SESP is missing | - | SESP is complete |Show if no data for project number or isSESP_Required false| Always show |
| **Delivery** | Delivery performance based on linear trendline analysis vs project timeline | Score <70% | Score 70-84% | Score 85%+ |Show if no data found for the project number| Always show |
| **Project Document** | Check if project document exists in the project document library | Cannot find project document | - | Project document found |-| Always show |
| **Project Board Meeting Minutes** | Check if project board meeting minutes exist in project document library | Cannot find meeting minutes | - | Meeting minutes found | - |Always show (ITM dependency) |
| **Missing Results** | Check if there are missing results for any output for previous years | Missing results detected | - | All results present |Show if no results data found for the project number| Always show |
| **Overdue Management Actions** | Check if there are overdue management actions from evaluations | Overdue actions exist | - | No overdue actions |Show if no evaluation data found for the project number| Always show |
| **SEQ Case** | Check if there is an open SEQ case (link to registry page) | Open SEQ case exists | - | - | - |Only show if open case exists |
| **SRM Case** | Check if there is an open SRM case (link to registry page) | Open SRM case exists | - | - | -|Only show if open case exists |
| **No Cost Extension** | Check if there is a no cost extension (show original close date and extension date) | - | Extension exists | - |-| Only show if extension exists |
| **Financial Closure** | Check if project is approaching or overdue for financial closure (counting from operational closure date) | Overdue for closure | Approaching closure | On track |Show if no data found for the project number| Always show |
| **LPAC** | Check if LPAC exists in the project document library | LPAC is missing | - | LPAC found |TBD| Always show |
| **Audit & HACT** | Show upcoming audits | TBD | TBD | TBD |TBD| Pending OAI data discussion |
| **Contributions** | Check if any payment tranches are overdue | TBD | TBD | TBD |TBD| Open question: how to handle multiple overdue tranches | 


## Programme & Project Management (PPM)
TBD

## Results Based Workplan
This section shows activity budget and result details by year for each output.

- **Task Number** -  Output 1,2...
- **Task Name** - Name of the task
- **Total Budget**  -  Total budget allocated for the task as the sum of tot_budget according to the year filter
- **Budget Delivery** - Total expenditure (the sum of tot_exp) / Total Budget 
- **Result Achivement** - The mean of completion percentages

**Activities**

- **Activities** - List of indicators and their budget details.
- **Activity Name** - ACTIVITY 1.1, ACTIVITY 1.2, ...
- **Activity BUdget Delivery** - The activity expenditure (The sum of tot_exp) / The activiy budget(the sum of tot_budget)
- **Expenditure Line Items** - The list of accounts and their amounts

**Results**


- **Indicator Code** - 1.1, 1.2 ,...
- **Indicator description** - Small description about the activity
- **Completion Details** - The actual result value over the target value
- **Result** - The average of the completions of activities under the task


## Funding Profile

- **Total Budget** - The sum of expense up to current year and budget of current year
- **Funded** – Funded amount by signed agreements
- **Unfunded** - ( Total budget - Funded )
 

### Funding Partners

- **Paid** - Summation of  Contribution Received per Donor
- **Remaining** - Summation of  Contribution Pending per Donor
- **Allocated** - Paid + Remaining per donor

### Payment Tranches

- **FundingPartnerName**: The name of the funding partner.
- **Amount**: The amount of the payment (`UN_Generate_AR_Invoices_Report` -> `RECEIPT_AMOUNT_USD_EQUIVALENT` and `UN_AR_Unbilled_Details_Report`->`USD_AMOUNT`).
- **Date**: The date of the payment (`UN_Generate_AR_Invoices_Report` -> `ACCOUNTING_DATE` and  `UN_AR_Unbilled_Details_Report`->`EVENT_DATE`  ) .
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