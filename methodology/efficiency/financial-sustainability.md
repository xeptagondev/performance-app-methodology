# Financial Sustainability Indicator

Note that this is a draft proposal for a new indicator.

## Introduction

The Financial Sustainability Indicator measures UNDP's ability to mobilize sufficient resources to meet the 2026-2029 Strategic Plan targets. This forward-looking indicator tracks the organization's progress toward securing approximately $17 billion in resources across the four-year planning period. By combining multiple funding streams and applying risk-adjusted discounts, this indicator provides a comprehensive view of UNDP's financial trajectory and identifies resource mobilization gaps that need to be addressed.

This indicator is critical for organizational planning as it enables proactive resource mobilization efforts, identifies funding shortfalls early, and ensures UNDP can deliver on its strategic commitments to member states and development partners.

## Organisational Objective

The organizational objective is to mobilize sufficient resources to fully fund the 2026-2029 Strategic Plan, targeting approximately $17 billion across the four-year period. This requires maintaining a steady pace of resource mobilization that accounts for both secured funding and projected pipeline opportunities, while managing the inherent uncertainty in future commitments.

## Data Components

The Financial Sustainability Indicator aggregates multiple funding streams and projections:

### 1. Secured Resources
- **UNDP Core Received & Projected**: Direct core funding received by UNDP from member states and partners
- **Contributions Received**: Actual contributions already received and recorded in financial systems
- **Signed Agreement Tranches**: Scheduled payments from existing signed agreements that will be received in future periods

### 2. Pipeline Resources (Risk-Adjusted)
Based on the existing pipeline methodology, opportunities are discounted according to their stage:

| Pipeline Stage | Policy Discount | Applied Discount Factor |
|----------------|-----------------|------------------------|
| Pipeline A (Hard) | 10% | 90% of value counted |
| Pipeline B (Soft) | 40% | 60% of value counted |
| Pipeline C (Ideas) | 70% | 30% of value counted |

### 3. Historical Pipeline Adjustment
An additional component accounts for opportunities not yet captured in the pipeline system. Based on backward analysis of signed agreements over recent years, this estimates the value of opportunities that typically emerge and progress to signature without being fully tracked through all pipeline stages. This "missing pipeline" estimate helps provide a more realistic projection of total resource mobilization potential.

### 4. Time-Based Discounting
For multi-year projections, an 8% annual discount rate is applied to future years to account for increasing uncertainty over time:
- Year 1 (2026): No discount
- Year 2 (2027): 8% discount
- Year 3 (2028): 15.36% discount (compounded)
- Year 4 (2029): 22.03% discount (compounded)

## Methodology

### Step 1: Calculate Annual Resource Projections

For each year in the strategic plan period (2026-2029), calculate total projected resources:

```
Annual Projected Resources = 
    UNDP Core Funding Received / Projected
    Contributions Received +
    Signed Agreement Tranches +
    (Pipeline A × 0.90) +
    (Pipeline B × 0.60) +
    (Pipeline C × 0.30) +
    Historical Pipeline Adjustment (20% Risk Buffer)
    Agency Services 
    GLOC
```

### Step 2: Apply Time-Based Discounting

Apply the discount factor based on how far in the future each year is:

```
Discounted Annual Resources = Annual Projected Resources × (1 - Discount Rate)^years_ahead
```

### Step 3: Calculate Resource Gap

Determine the gap between projected resources and strategic plan targets:

```
Annual Gap = Annual Target - Discounted Annual Resources
Total Gap = Sum of all Annual Gaps (2026-2029)
```

### Step 4: Calculate Monthly Mobilization Target

Divide the total gap by the number of months remaining in the strategic plan period:

```
Monthly Mobilization Target = Total Gap / Months Remaining Until End of 2029
```

This creates a linear trendline representing the required monthly resource mobilization pace.

### Step 5: Track Actual Performance

Each month, compare actual resource mobilization against the trendline:

```
Monthly Performance = (Actual Resources Mobilized / Monthly Target) × 100
```

## Scoring Methodology

The scoring system follows a similar approach to the Delivery indicator, using a trendline-based assessment with penalties for underperformance:

### Base Score Calculation
- **Meeting or Exceeding Trendline**: 100 points
- **Below Trendline**: For every 1% below the target trendline, deduct 2 points from the base score

### Final Score Calculation
```
Final Score = Base Score
```
The final score is capped at 100 and cannot go below 0.

## Traffic Light System

| Traffic Light | Score | Interpretation |
|---------------|-------|----------------|
| Green | 85+ | On track to meet strategic plan targets |
| Yellow | 70-84 | At risk; increased mobilization efforts needed |
| Red | <70 | Significant gap; urgent action required |

