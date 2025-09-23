# Pipeline

{% hint style="info" %}
This is a draft proposal for a new indicator.
{% endhint %}

## Introduction

The pipeline indicator measures the health of the number and value of all the potential agreements. This is perhaps the most critical indicator for financial sustainability at UNDP because it dictates the future resources available for mobilization in projects, programmes, and portfolios for years to come. 

The data for this comes from Unity which is part of Quantum+ (i.e. Salesforce). All Country Offices (COs) and Central Bureaus (CBs) use Unity to log new opportunities and update the pipeline stage as opportunities progress. 

When an opportunity is created, it typically goes through various different pipeline stages. 

1. **Pipeline C (Ideas):** This is a speculative opportunity that is not yet ready to be considered for funding. Typically will not result in a project within the next 12 months. 
2. **Pipeline B (Soft Pipeline):** This is an opportunity that is ready to be considered for funding, but the funding is not yet guaranteed. Should be closing in the next 12 months. 
3. **Pipeline A (Hard Pipeline):** This is an opportunity that is under active negotiation and is likely to be signed soon. Should be closed in the next 6 months. 
4. **Signed Agreement:** This is an opportunity that has been signed and is now an actual agreement.

There are actually more stages in the pipeline data, but we do not consider them all:

| Stage                                   | Used in Methodology? |
|-----------------------------------------|-----------------------|
| Agreement Signed (100%)                 | Yes                   |
| Withdrawn/Discontinued                  | No                    |
| C- Ideas (30%)                          | Yes                   |
| B-Soft Pipe Line (50-70%)              | Yes                   |
| A-Hard Pipeline (90%)                   | Yes                   |
| Exploratory Opportunity                  | No                    |
| Withdrawn                                | No                    |
| Agreement Signed / Engagement Achieved   | Yes                   |
| Initial Meetings                         | No                    |
| Negotiations / Contracting               | No                    |
| Formulation, Planning & Coordination     | No                    |
| Engagement Not Achieved                  | No                    |
| Proposal Development                     | No                    |

Each pipeline stage has a discount as shown in this table:

| Pipeline Stage | Policy Discount | Actual Discounts |
| -------------- | --------------- | ----------------- |
| C              | 70%             | 80%               |
| B              | 40%             | 60%               |
| A              | 10%             | 35%               |
| Signed         | 0%              | 0%              |

The average policy discount across pipeline stages is 30%, while the average actual discount is 43.75%. 

This discount applies to the total value of the agreement and the tranches (i.e. payments that will be made from donors to UNDP each year if the agreement is signed) when calculating the potential future cash flows arising from the opportunity. Based on a historical analysis of close rates, we also have "actual" discounts for each pipeline stage that offer a more realistic picture of the likely amount of resources available to UNDP based on the current snapshot of the health of the pipeline. In the future, the policy discounts should be updated to the actual discounts as they become more accurate over time.

**The Performance App will use the policy discounts to calculate the pipeline indicator.**



## Organisational Objective

The organizational objective is, at a minimum, to replenish delivery in future years, accounting for inflation. The ideal scenario is the total value of the pipeline is growing month on month to support the growth in contributions and delivery in future years. 


## Data

Table names in UNDP Data Warehouse: [SF_UNITY].[Opportunity]

The columns from the Data Warehouse are the following:

* **Department**: The organizational unit or office within UNDP.
* **Opportunity Record Type**: The type of opportunity, such as funding, non-funding, exploratory. 
* **Opportunity Name**: The name or title of the opportunity.
* **Organisation Name**: The name of the organization offering or involved in the opportunity.
* **Opportunity Owner**: The person responsible for managing or overseeing the opportunity.
* **Initial Stage**: The initial stage (A/B/C) of the opportunity when it was first recorded.
* **Stage**: The current stage (A/B/C/Signed) of the opportunity.
* **Close Date**: The projected or actual signature date of the financial agreement.
* **Description**: A brief description of the opportunity.
* **Funding Stream**: The source of funding or type of financial support for the opportunity.
* **Opportunity Currency**: The currency in which the opportunity's financials are denoted.
* **Total Target Funding (OR)**: The total target funding amount for the opportunity. This is non-discounted and non-core (i.e. no TRAC funds are included here)
* **Implementation Period**: The timeframe over which the opportunity is to be implemented. Note, this is based on the tranche payments, the actual project end date could be different. 
* **YR2022** to **YR2030**: Yearly breakdown of expected tranche payments. Each year, we add another future year. 
* **Status**: The current status of the opportunity, such as Prodoc being developed, no clear donor prospect, etc. These are more detailed than the pipeline stage, but do not affect the calculation of the pipeline. 
* **Details/Status**: Additional details or updates on the current status of the opportunity.
* **Next Step**: The next steps or actions required for the opportunity.
* **Last Note/Status**: The most recent note or update on the opportunity's status.
* **Thematic Team**: The team, cluster, or thematic area associated with the opportunity.
* **Topic List**: A list of topics or areas of focus related to the opportunity.
* **External Partner Contacts**: Contacts at external partner organizations involved in the opportunity.
* **Implementing Partners**: The organizations responsible for implementing the opportunity.
* **Responsible Parties**: The parties or individuals responsible for various aspects of the opportunity.
* **Target Countries**: The countries targeted by the opportunity.
* **Created Date**: The date when the opportunity record was created.
* **Created By**: The individual who created the opportunity record.
* **Last Modified Date**: The date when the opportunity record was last modified.
* **Last Modified By**: The individual who last modified the opportunity record.
* **Id**: Unique identifier for the opportunity record.
* **IsDeleted**: Boolean flag indicating if the record has been deleted.
* **AccountId**: Unique identifier linking to the associated account/organization.
* **RecordTypeId**: Identifier for the type of opportunity record.
* **IsPrivate**: Boolean flag indicating if the opportunity is private.
* **Name**: Name of the opportunity.
* **StageName**: Current stage name of the opportunity.
* **Amount**: Financial amount associated with the opportunity.
* **Probability**: Probability percentage of winning the opportunity.
* **ExpectedRevenue**: Calculated expected revenue based on amount and probability.
* **TotalOpportunityQuantity**: Total quantity associated with the opportunity.
* **Type**: Type classification of the opportunity.
* **LeadSource**: Source of the opportunity lead.
* **IsClosed**: Boolean flag indicating if the opportunity is closed.
* **IsWon**: Boolean flag indicating if the opportunity was won.
* **ForecastCategory**: Category for forecasting purposes.
* **ForecastCategoryName**: Name of the forecast category.
* **CampaignId**: Identifier linking to associated campaign.
* **HasOpportunityLineItem**: Boolean flag indicating if opportunity has line items.
* **Pricebook2Id**: Identifier linking to associated pricebook.
* **OwnerId**: Identifier of the opportunity owner.
* **CreatedById**: Identifier of user who created the record.
* **LastModifiedById**: Identifier of user who last modified the record.
* **SystemModstamp**: System timestamp of last modification.
* **LastActivityDate**: Date of last activity on the opportunity.
* **FiscalQuarter**: Fiscal quarter of the opportunity.
* **FiscalYear**: Fiscal year of the opportunity.
* **Fiscal**: Fiscal period information.
* **ContactId**: Identifier linking to associated contact.
* **LastViewedDate**: Date the record was last viewed.
* **LastReferencedDate**: Date the record was last referenced.
* **ContractId**: Identifier linking to associated contract.
* **HasOpenActivity**: Boolean flag indicating if there are open activities.
* **HasOverdueTask**: Boolean flag indicating if there are overdue tasks.
* **Account_Implementing_Partner__c**: Implementing partner account information.
* **Account_Responsible_Party__c**: Responsible party account information.
* **CPD_Outcome_Primary__c**: Primary Country Programme Document outcome.
* **CPD_Output_Primary__c**: Primary Country Programme Document output.
* **Change_Opportunity_Type__c**: Field tracking opportunity type changes.
* **Closed_Reason_NonFunding__c**: Reason for closure for non-funding opportunities.
* **Closed_Reason__c**: General reason for opportunity closure.
* **Create_a_New_Opportunity__c**: Field related to new opportunity creation.
* **I_am_in_the_Owners_Initiative_Region__c**: Boolean indicating regional ownership match.
* **I_am_in_the_Owners_Region__c**: Boolean indicating regional ownership match.
* **Include_on_Funding_Pipeline__c**: Boolean for inclusion in funding pipeline.
* **Managing_Department__c**: Department managing the opportunity.
* **Next_Opportunity_Review_Date__c**: Date of next scheduled review.
* **Opp_Name_Text__c**: Text version of opportunity name.
* **Opportunity_ID__c**: Custom opportunity identifier.
* **Opportunity_Lead_Name__c**: Name of opportunity lead.
* **Partnership_Strategy__c**: Strategy for partnership development.
* **Project_ID__c**: Associated project identifier.
* **Project_Type__c**: Type classification of project.
* **Targeted_Countries__c**: Countries targeted by the opportunity.
* **Thematic_Area_Programmatic_Area__c**: Thematic or programmatic area classification.
* **Thematic_TeamV2__c**: Updated thematic team assignment.
* **UNDP_Signature_Solution__c**: UNDP signature solution classification.
* **Opportunity_Development_Total_Cost__c**: Total cost of opportunity development.
* **Target_Fund_Next_Year__c**: Target funding for next year.
* **Target_Funding_Future_Years__c**: Target funding for future years.
* **Total_Funding_This_Year__c**: Total funding for current year.
* **Total_Target_Funding__c**: Total target funding amount.
* **CPD_YR1__c**: Country Programme Document Year 1 data.
* **CPD_YR2__c**: Country Programme Document Year 2 data.
* **CPD_YR3__c**: Country Programme Document Year 3 data.
* **CPD_YR4__c**: Country Programme Document Year 4 data.
* **CPD_YR5__c**: Country Programme Document Year 5 data.
* **Contact_List_Rollup__c**: Rolled up list of contacts.
* **Stage_Modified_Date__c**: Date of last stage modification.
* **Expected_Agreement_Duration__c**: Expected duration of agreement.
* **Expected_Agreement_Start__c**: Expected start date of agreement.
* **Organization_Subtype__c**: Subtype classification of organization.
* **Exploratory_Type_Change_Date__c**: Date of exploratory type change.
* **Day_of_the_Month__c**: Day of month field.
* **Department_Name__c**: Name of department.
* **Opportunity_Name__c**: Custom opportunity name field.
* **Ultimate_Parent_Organization__c**: Ultimate parent organization name.
* **Ultimate_Parent_ID__c**: Identifier of ultimate parent organization.
* **Organisation_Subtype__c**: Subtype of organization.
* **Opp_Team_List__c**: List of team members.
* **Target_Countries_List_255__c**: List of target countries (255 char limit).
* **Cloned_record__c**: Boolean indicating if record is cloned.
* **Add_Supporting_Thematic_Teams__c**: Field for additional thematic teams.
* **Organisation_Source__c**: Source of organization data.
* **W_INSERT_DT**: Warehouse insert date.
* **W_CREATED_BY**: Warehouse record creator.
* **W_UPDATE_DT**: Warehouse update date.
* **W_UPDATED_BY**: Warehouse record updater.

## Data Export

## Methodology

The pipeline indicator is scored based on two main categories, each contributing to the final score:

1. **Pipeline Sizing**: Ensures the pipeline is adequately sized to meet future programme delivery and office financial sustainability goals.
2. **Pipeline Health**: Assesses the accuracy and active management of the pipeline within Unity. 

This approach provides a comprehensive view of both the pipeline's capacity to meet replenishment goals and its realistic representation of available opportunities.

### Part 1: Pipeline Sizing (70%)

Pipeline Sizing is calculated as a weighted sum of three components:

#### A) Active Pipeline Size (65%)
This measures the total discounted value of all pipeline opportunities in Pipeline A, B, and C against 200% of the average delivery over the last 3 calendar years. For example, in 2025, the average delivery would be calculated using the years 2024, 2023, and 2022. The ratio of 200% has been chosen because the pipeline is the main source of replenishment of delivery for UNDP.

In essence, pipeline *is* future delivery, but opportunities typically take 1-2 years to be signed and another 1-2 years to be delivered. 


#### B) Total Value of Signed Agreements (25%)
This component measures the total value of resources that have been mobilized from signed opportunities in the current year-to-date (YTD). The calculation takes the ratio of resources mobilized to the previous year's delivery amount. This ratio is then evaluated against the delivery trendline from the previous year to provide context for the current year's performance. The resulting rate directly determines the subindicator score.

For example, if an office mobilized $10M in resources YTD and had $8M in delivery the previous year, their ratio would be 125%. This ratio would then be compared to their historical delivery trends to determine if they are on track to meet their resource mobilization targets. The final score reflects how well they are maintaining or growing their resource base relative to delivery needs.


#### C) Median Opportunity Size (10%)
This component evaluates the growth in typical opportunity size by comparing the median size of current pipeline opportunities to the previous year's median. We specifically use the median rather than the mean project size because the median is more resistant to being skewed by extremely large projects. This provides a more accurate representation of the "typical" project size that offices are pursuing, as a few very large projects could artificially inflate an average-based metric.

The baseline expectation is for offices to grow their median project size year over year, which encourages a gradual shift toward larger, more strategic interventions while maintaining a diverse portfolio. This growth in project size often indicates increased donor confidence and improved operational capacity to manage larger initiatives.

The scoring is straightforward: if the current year's median project size exceeds the previous year's median, the office receives a full 100% score for this component. If the median size has decreased, the score is calculated as the ratio of the current year's median to the previous year's median, expressed as a percentage. For example, if the median project size fell from $1M to $800K, the score would be 80%.


### Part 2: Pipeline Health (30%)

Pipeline Health is assessed through three components:

#### A) Opportunity Age (30%)
The average age of opportunities in the pipeline is a critical metric in pipeline health. In CRM systems, opportunity age helps identify stagnation and potential issues in the sales or resource mobilization process. Opportunities that remain in the pipeline for extended periods often indicate either unrealistic prospects or insufficient follow-up, both of which can waste organizational resources and provide inaccurate forecasting data.

For UNDP's pipeline management, we measure the average age of all opportunities, with newer opportunities receiving higher scores. This scoring approach reflects the understanding that healthy pipelines maintain a steady flow of opportunities moving through various stages. The scoring system is structured as follows:

| Months       | Score   |
|--------------|---------|
| Below 12     | 100/100 |
| 12 to 18    | 75/100  |
| 18 to 24    | 50/100  |
| Above 24     | 25/100  |

Opportunities less than 12 months old receive a perfect score of 100/100, recognizing that most viable opportunities should progress to signing or closure within a year. Opportunities between 12-18 months receive 75/100, while those between 18-24 months score 50/100. Any opportunities remaining in the pipeline beyond 24 months receive only 25/100, signaling a need for review or removal. In cases where an operating unit has no opportunities in their pipeline, they receive a score of 0/100, reflecting the critical importance of maintaining an active opportunity pipeline.


#### B) Opportunity Activity (30%)
Opportunity Activity measures how frequently pipeline opportunities are being reviewed and updated, which is a key indicator of active pipeline management. Regular updates demonstrate that opportunities are being actively monitored and pursued rather than sitting dormant in the system.

The calculation is straightforward:
- First, we identify all opportunities that have been updated within the last 3 months
- Then, we calculate what percentage these recently updated opportunities represent of the total pipeline
- This percentage directly translates to the score (e.g. if 75% of opportunities were updated in the last 3 months, the score is 75/100)

For example, if an office has 20 total opportunities and 15 of them were updated in the last 3 months, their Opportunity Activity score would be 75/100.

Updates include any modifications to the opportunity record, not just a change in the pipeline stage. For example:

- Changes to expected value
- Modifications to expected signing date
- New notes or attachments
- Status changes between pipeline stages


#### C) Early Stage Capture Rate (40%)
The Early Stage Capture Rate measures how effectively offices are identifying and tracking potential opportunities from their earliest stages. Specifically, it calculates the percentage of successfully signed opportunities that were initially created in Pipeline C (also known as "Initial: Exploratory Opportunity"). This metric is crucial for UNDP's organizational forecasting and resource planning.

For example, if an office signs 10 projects in a year, and 7 of those projects were originally captured and tracked from Pipeline C stage, their Early Stage Capture Rate would be 70%. To prevent gaming of this metric, opportunities must remain in Pipeline C for at least 14 days before progressing through subsequent pipeline stages (Pipeline B, Pipeline A, and finally Signed). This minimum duration requirement ensures that opportunities are genuinely being identified and managed from their early stages, rather than being artificially pushed through the pipeline stages.

Early identification and tracking of opportunities is vital for UNDP's organizational effectiveness. When opportunities are captured early, it enables better resource planning, more accurate financial forecasting, and increased potential for cross-country collaboration. Early tracking allows country offices to share information about emerging opportunities, potentially leading to multi-country initiatives or knowledge sharing that strengthens project design. Additionally, comprehensive early-stage pipeline data helps UNDP leadership make more informed decisions about resource allocation and strategic priorities across the organization.

 

### **Overall Calculation**

* **Part 1: Pipeline Sizing (70%)**
  * **A:** Active Pipeline Size (65%)
  * **B:** Total Value of Signed Agreements (25%)
  * **C:** Median Opportunity Size (10%)

* **Part 2: Pipeline Health (30%)**
  * **A:** Opportunity Age (30%)
  * **B:** Opportunity Activity (30%)
  * **C:** Early Stage Capture Rate (40%)

* **Final Score Calculation:** The final score combines these parts, weighted accordingly:
  * Part 1 contributes 70%.
  * Part 2 contributes 30%.




## Traffic Light System

| Traffic Light | Score |
| ------------- | ----- |
| Green         | 80+   |
| Yellow        | 60+   |
| Red           | <60   |

## Subsection Scoring Thresholds

| Subsection                                      | Red      | Orange    | Green    |
|-------------------------------------------------|----------|-----------|----------|
| Active Pipeline Size                            | 0–59     | 60–79     | 80–100   |
| Total Value of Signed Agreements                | 0–95     | 96–99     | 100      |
| Median Opportunity Size                         | 0–59     | 60–79     | 80–100   |
| Average Opportunity Age                         | 0–59     | 60–79     | 80–100   |
| Opportunities with activity in last 3 months    | 0–59     | 60–79     | 80–100   |
| Early Stage Capture Rate                        | 0–59     | 60–79     | 80–100   |



## Limitations 

- The system does not count Central Bureau opportunities correctly if the funds are allocated to multiple departments (i.e. typically country offices or HQ departments). Unity team is working on a feature to fix this by introducing a parent-subsidiary relationship for opportunities. 


## Resources

- Unity Platform
- [Pipeline Policy Guide](https://view.officeapps.live.com/op/embed.aspx?src=https://popp.undp.org/sites/g/files/zskgke421/files/2023-09/FRM_Pipeline%20Management_Guidelines.docx)


