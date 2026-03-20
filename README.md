# dealer-credit-risk-monitoring
Dealer credit exposure monitoring using percentile-based segmentation and Tableau dashboard

## Business Problem
Companies that extend trade credit to dealers face the risk of delayed payments and excessive credit exposure. Monitoring dealer-level exposure is critical to identify high-risk accounts and take timely credit control actions.

## Objective
To build a credit risk monitoring system that analyzes dealer exposure and identifies high-risk accounts using portfolio-based segmentation.

## Approach
- Used percentile-based segmentation to handle skewed exposure data  
- Built a utilization-driven risk model instead of static threshold classification  
- Designed a conservative system to prioritize early risk detection over breach detection  

## Dataset
- Source: Simulated dealer-level credit dataset (inspired by Kaggle-style transactional data)  
- Data includes:
  - Dealer transactions  
  - Invoice details  
  - Outstanding amounts  
- Note: Credit limits were not present in the dataset and were derived analytically  

## Methodology
### 1. Data Preparation
- Raw dataset imported using Power Query  
- Data cleaned and transformed in Excel  
- Aggregated dealer-level metrics such as:
  - Total Outstanding  
  - Invoice Count  
  - Oldest Invoice Date  

### 2. Exposure-Based Segmentation
- Calculated percentile thresholds (P25, P50, P75, P90, P95)  
- Dealers segmented based on exposure distribution:

| Percentile Range | Limit Bucket |
|-----------------|--------------|
| < P25 | Low |
| P25 – P75 | Medium |
| P75 – P90 | High |
| P90 – P95 | Very High |
| > P95 | Exception |

### 3. Credit Limit Simulation
- Since no predefined credit limits were available, system credit limits were derived using percentile-based segmentation  
- Assigned limits:
  - Low → 2000  
  - Medium → 4000  
  - High → 7000  
  - Very High → 9000  
  - Exception → No system limit (manual approval required)  

### 4. Utilization-Based Risk Framework
- Utilization calculated as:  
  **Utilization = Total Outstanding / System Credit Limit**
- Risk flags assigned based on thresholds:
  - ≤50% → Low Risk  
  - ≤75% → Moderate Risk  
  - ≤90% → High Risk  
  - >90% → Critical Risk  

## Credit Control Framework

| Risk Level | Recommended Action |
|-----------|------------------|
| Low | Normal operations |
| Moderate | Increase monitoring frequency |
| High | Tighten terms/partial dispatch |
| Critical | Stop dispatch untill exposure reduces |
| Exception | Credit committee approval required |

## Dashboard Overview (Tableau)
- Total Outstanding   
- Total Credit Limit  
- Utilization  
- Dealer Count by Risk  
- Exposure by Risk
- Exposure vs System Limit 

## Tools Used
- Excel (Power Query, Data Analysis)  
- Tableau (Dashboard Visualization)  

## Key Insights
- Risk is concentrated in a small set of high-exposure dealers (long-tail distribution)  
- Majority of dealers operate within conservative credit limits, indicating buffer in the system  
- Exception segment represents dealers exceeding modeled thresholds, requiring manual intervention  
- Portfolio utilization highlights early warning signals before actual credit breaches occur  

## Tableau Dashboard
https://public.tableau.com/views/DealerCreditRiskMonitoringDashboard/DealerCreditRiskMonitoring?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link

## Project Structure
- `data/` → Raw dataset  
- `excel/` → Data processing and risk logic  
- `dashboard/` → Tableau dashboard  

## Note
- Dataset used is simulated and created for demonstration purposes  
- Credit limits are analytically derived and represent monitoring thresholds, not sanctioned limits  
- The dashboard is designed for portfolio-level risk monitoring, not collections tracking (DPD/aging excluded intentionally)
- Dataset used is simulated and created for demonstration purposes  
- Credit limits are analytically derived and represent monitoring thresholds, not sanctioned limits  
- The dashboard is designed for portfolio-level risk monitoring, not collections tracking (DPD/aging excluded intentionally)  
