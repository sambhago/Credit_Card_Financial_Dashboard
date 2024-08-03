# Credit Card Financial Dashboard

**Project Objective:**
To develop a comprehensive credit card weekly dashboard that provides real-time insights into key performance metrics and trends, enabling stakeholders to monitor and analyze credit card operations effectively.

**DAX Queries**

```DAX
AgeGroup = SWITCH(
 TRUE(),
 'public cust_detail'[customer_age] < 30, "20-30",
 'public cust_detail'[customer_age] >= 30 && 'public cust_detail'[customer_age] < 40, "30-40",
 'public cust_detail'[customer_age] >= 40 && 'public cust_detail'[customer_age] < 50, "40-50",
 'public cust_detail'[customer_age] >= 50 && 'public cust_detail'[customer_age] < 60, "50-60",
 'public cust_detail'[customer_age] >= 60, "60+",
 "unknown"
 )

IncomeGroup = SWITCH(
 TRUE(),
 'public cust_detail'[income] < 35000, "Low",
 'public cust_detail'[income] >= 35000 && 'public cust_detail'[income] <70000, "Med",
 'public cust_detail'[income] >= 70000, "High",
 "unknown"
)

week_num2 = WEEKNUM('public cc_detail'[week_start_date])

Revenue = 'public cc_detail'[annual_fees] + 'public cc_detail'[total_trans_amt] + 'public cc_detail'[interest_earned]

Current_week_Reveneue = CALCULATE(
 SUM('public cc_detail'[Revenue]),
 FILTER(
 ALL('public cc_detail'),
 'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])))

Previous_week_Reveneue = CALCULATE(
 SUM('public cc_detail'[Revenue]),
 FILTER(
 ALL('public cc_detail'),
 'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])-1))
```

## Project Insights - Week 53 (31st Dec)

### Week-over-Week Change:
- **Revenue increased by 28.8%**
- **Total Transaction Amount & Count increased by xx% & xx%**
- **Customer count increased by xx%**

### Year-to-Date Overview:
- **Overall revenue:** $57M
- **Total interest:** $8M
- **Total transaction amount:** $46M
- **Male customers contributed more to revenue:** $31M compared to $26M from female customers
- **Blue & Silver credit cards accounted for 93% of overall transactions**
- **Top contributing states:** TX, NY, and CA with 68%
- **Overall activation rate:** 57.5%
- **Overall delinquency rate:** 6.06%
