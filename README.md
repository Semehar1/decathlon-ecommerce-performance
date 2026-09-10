# Decathlon E-Commerce Performance Analytics

![Power BI](https://img.shields.io/badge/Power%20BI-Analytics-F2C811?logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-Time%20Intelligence-blue)
![Data Modeling](https://img.shields.io/badge/Data%20Model-Star%20Schema-0F766E)
![Status](https://img.shields.io/badge/Status-Completed-2E7D32)

An executive Power BI dashboard analyzing Decathlon e-commerce performance across sales, profitability, orders, products, geography, and sales channels.

This project was built as an end-to-end BI exercise: starting with a structured sales dataset, developing a star-schema model and DAX measures, and turning the results into a concise executive dashboard.

## Dashboard

![Decathlon E-Commerce Performance Dashboard](screenshots/dashboard.png)

## Business Questions

The dashboard is designed to answer:

- How much revenue and profit are being generated?
- How are sales trending over time?
- How does current sales performance compare with last year?
- Which product categories generate the most sales?
- Which countries and cities contribute most to sales?
- Which sales channels are driving revenue?

## Executive KPI Snapshot

| KPI | Result |
|---|---:|
| Total Sales | **€3.81M** |
| Total Profit | **€1.50M** |
| Total Orders | **10K** |
| YoY Growth | **49%** |

## Key Findings

### Product categories
Tennis is the strongest category at approximately **€0.57M**, followed by Fitness (**€0.55M**) and Hiking & Camping (**€0.53M**).

### Sales channels
**Online** is the dominant channel at approximately **€1.71M**, followed by Mobile App (**€0.96M**) and Click & Collect (**€0.77M**).

### Geographic performance
**France** is the largest market at approximately **€0.97M**, followed by Spain (**€0.62M**) and Germany (**€0.59M**).

### Trend
The dashboard compares monthly sales with the previous year and provides a high-level view of sales momentum over time.

## Dashboard Design

The final page uses four complementary analytical views:

1. **Sales trend** — monthly sales and prior-year comparison
2. **Category performance** — sales by product category
3. **Geographic performance** — sales by country and city
4. **Channel performance** — sales by e-commerce channel

A geographic treemap was used instead of the earlier duplicate category visual so the page covers four distinct business dimensions rather than repeating essentially the same ranking twice.

## Data Model

The workbook uses a star-schema practice model with a central sales fact table and supporting dimensions.

### Fact table
- Sales / transaction-level data
- Order ID
- Customer key
- Product key
- Channel key
- Promotion key
- Order date
- Sales and cost measures

### Dimensions
- **Date**
- **Customer**
- **Product**
- **Channel**
- **Promotion**

This structure supports reusable DAX measures and consistent filtering across the report.

## DAX

Core measures used in the report include:

```DAX
Total Sales =
SUM(tbl_Sales[NetSales])
```

```DAX
Total Orders =
DISTINCTCOUNT(tbl_Sales[OrderID])
```

```DAX
Sales LY =
CALCULATE(
    [Total Sales],
    SAMEPERIODLASTYEAR('Date'[Date])
)
```

```DAX
Sales YoY % =
DIVIDE(
    [Total Sales] - [Sales LY],
    [Sales LY]
)
```

> The exact table/column names should be checked against the included PBIX if the model is reused in another file.

## Tools & Skills

**Tools**
- Power BI
- DAX
- Excel

**Skills demonstrated**
- Star-schema data modeling
- Data preparation
- KPI development
- DAX measures
- Time-intelligence calculations
- Year-over-year analysis
- Product/category analysis
- Geographic analysis
- Channel analysis
- Dashboard UX and visual storytelling

## Repository Contents

```text
decathlon-ecommerce-performance/
│
├── README.md
├── LICENSE
├── .gitignore
│
├── powerbi/
│   └── Decathlon_Ecommerce_Performance.pbix
│
├── data/
│   └── Decathlon_PL300_StarSchema_Practice.xlsx
│
└── screenshots/
    └── dashboard.png
```

## How to Use

1. Download or clone the repository.
2. Open `powerbi/Decathlon_Ecommerce_Performance.pbix` in Power BI Desktop.
3. Review the model, measures, relationships, and report page.
4. If the source workbook is moved, update the Power BI data-source path.

## Notes

This is a portfolio/practice analytics project. The dashboard is intended to demonstrate BI workflow, data modeling, DAX, and business storytelling rather than represent Decathlon's actual public financial reporting.

## Author

**Data Analytics Portfolio Project**

Power BI • DAX • Data Modeling • Business Intelligence
