# ABC Company Sales Dashboard – Power BI & Python EDA

**Project Overview**  
This repository contains a complete end-to-end sales analytics solution for **ABC Company**, covering **three years (2017–2019)** of transactional data. The goal is to deliver actionable insights into **sales performance**, **customer coverage**, **product trends**, and **target achievement** through a professional Power BI dashboard and supporting Python-based exploratory data analysis (EDA).

The dashboard enables leadership to:
- Track **revenue & unit growth** year-over-year  
- Identify **top-performing products, categories, and salespeople**  
- Monitor **target achievement % (revenue vs. target)**  
- Visualize **geographic concentration** (city/state)  
- Navigate **year-specific metric pages** (2017 | 2018 | 2019)  

---

## Key Business Insights
| Metric | 2017 | 2018 | 2019 (Partial) |
|-------|------|------|----------------|
| **Revenue** | $6.65M | $10.21M (+54%) | $1.05M |
| **Units Sold** | 1.05M | 1.58M (+50%) | 0.16M |
| **Target Achievement (Rev vs. Monthly Target)** | 41% | 63% | 8% |
| **Top Category** | Food (58%) | Food (60%) | Food (55%) |
| **Geographic Coverage** | 100% Washington | 100% Washington | 100% Washington |

> **2019 data is partial (December only)** – projections unavailable.

---

## Project Workflow

### 1. **Data Acquisition & Loading**  
- Loaded **Sales 2017/2018/2019.xlsx**  
- Imported **DimensionTables.xlsx** (Customers, Products, ProductGroups, SalesPersons, Dates)  
- Imported **Targets.xlsx** (monthly & annual targets per salesperson)

### 2. **Python EDA (Colab Notebook)**  
- **Merged** fact (Sales) + dimension tables on respective IDs  
- **Cleaned & Transformed**:  
  - Standardized column names  
  - Calculated `sales_amount = quantity × unit_price`  
  - Created `geo location = city + ", " + state`  
  - Built `date` column (full datetime) from month/day/year  
- **Validated**: No unmatched customers, 1,272 unique customers, all in WA  
- Exported cleaned dataset: `ABC_data.csv`

### 3. **Power BI Data Modeling & Transformation**  
- Imported `ABC_data.csv`  
- **Transformed Targets**:  
  - Removed metadata rows  
  - Unpivoted monthly targets → long format  
  - Created `Year`, `Month`, `Monthly Target`, `Annual Target`  
- **Relationships**:  
  - `ABC_data[SalesPerson ID]` → `Targets[SalesPerson ID]`  
  - `ABC_data[date]` → `Dates[dates]` (optional for time intelligence)

### 4. **DAX Measures**  
Examples:
Total Revenue = SUM(ABC_data[sales_amount])
Total Units Sold = SUM(ABC_data[quantity])
Total Target = SUM(Targets[Monthly Target])
Revenue Target Achievement % = 
    DIVIDE([Total Revenue], [Total Target])

###5. **Dashboard Design**

Main Page: High-level KPIs + navigation
Year Pages (2017 | 2018 | 2019):

Page-level filters applied via date[Year]
Visuals: Line charts (trend), Donut (category), Map (geo location), KPI cards


Navigation: Buttons linking between pages
/
├── ABC_data.csv                  # Cleaned fact + dimension merge
├── Copy of ABC Sales EDA.ipynb   # Full Python EDA notebook
├── ABC_Sales_Dashboard.pbix      # Final Power BI file
├── Sales 2017.xlsx               # Raw sales data
├── Sales 2018.xlsx
├── Sales 2019.xlsx
├── DimensionTables.xlsx          # Customers, Products, etc.
├── Targets.xlsx                  # Monthly & annual targets
└── README.md                     # This file

How to Use

Open ABC_Sales_Dashboard.pbix in Power BI Desktop
Explore the main dashboard
Use navigation buttons to view 2017 / 2018 / 2019 metrics
Adjust slicers (optional) for deeper drill-down


Python notebook is for reproducibility and data validation

Recommendations

Expand beyond Washington – 100% geographic risk
Load full 2019 data for accurate YoY analysis
Incentivize underperformers (bottom 3 salespeople < $1M each)
Capitalize on Q4 seasonality (30–35% of annual revenue)
Focus marketing on top 10 products (42% of sales)


Tech Stack

Python: pandas, numpy, matplotlib, seaborn
Power BI: Power Query (M), DAX, Data Modeling, Visualizations
Tools: Google Colab, GitHub


Author: [Christopher Mauro]
Date: October 2025
Portfolio Project – Data Analytics & Business Intelligence
