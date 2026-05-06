# Telecom Customer Churn Analysis

Power BI dashboard + Python analysis identifying churn drivers in a telecom dataset of 7,043 customers. Built during internship at Saiket Systems.

## Dashboard Overview

![Churn Dashboard](Customer%20churn%20analysis/dashboard_preview.png)

**Overall churn rate: 26.5%** — significantly above industry benchmark of 15–20%

## Key Findings

| Segment | Churn Rate | Insight |
|---------|-----------|---------|
| Month-to-month contracts | 42.7% | vs 11% annual — contract type is #1 predictor |
| Fiber optic customers | 41.9% | Higher churn despite premium service — price sensitivity |
| No tech support | 41.6% | Support access significantly reduces churn |
| Senior citizens | 41.7% | Underserved segment needing simpler plans |
| Tenure < 1 year | 47.4% | First year is critical retention window |

## Churn Predictors (ranked by correlation)
1. Contract type (month-to-month vs annual)
2. Tenure — longer customers churn less
3. Tech support availability
4. Internet service type
5. Monthly charges — higher bill = higher churn

## Python Analysis

```python
import pandas as pd
import matplotlib.pyplot as plt

df = pd.read_excel('Telco_Customer_Churn_Dataset_raw.xlsx')

# Churn by contract type
churn_by_contract = df.groupby('Contract')['Churn'].apply(
    lambda x: (x == 'Yes').mean() * 100
).round(1)
print(churn_by_contract)
# Month-to-month    42.7%
# One year          11.3%
# Two year           2.8%

# Revenue at risk from churned customers
monthly_revenue_lost = df[df['Churn'] == 'Yes']['MonthlyCharges'].sum()
print(f"Monthly revenue at risk: ${monthly_revenue_lost:,.0f}")
```

## Recommendations
1. **Offer contract migration incentives** — move MTM customers to annual at 10–15% discount
2. **First-90-day onboarding** — proactive outreach to customers in critical churn window
3. **Bundle tech support** — customers with support churn at half the rate

## Stack
- **Power BI** — Interactive dashboard with slicers by demographics, contract, service
- **Python** — pandas, matplotlib, seaborn for exploratory analysis
- **Dataset** — IBM Telco Customer Churn (7,043 customers, 21 features)
