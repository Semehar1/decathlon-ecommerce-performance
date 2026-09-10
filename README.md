# Decathlon E-Commerce Performance Analytics

![Power BI](https://img.shields.io/badge/Power%20BI-Analytics-F2C811?logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-Time%20Intelligence-blue)
![Data Modeling](https://img.shields.io/badge/Data%20Model-Star%20Schema-0F766E)
![Status](https://img.shields.io/badge/Status-Completed-2E7D32)

An executive Power BI dashboard analyzing e-commerce performance across sales, profitability, orders, products, geography, and sales channels.

Built as a practical companion to my Microsoft PL-300 Power BI Data Analyst certification preparation, this project demonstrates an end-to-end BI workflow: structured data, star-schema modeling, DAX measures, time-intelligence analysis, KPI development, and executive dashboard storytelling.

---

## 📌 TL;DR

The analysis shows **€3.81M in Net Sales**, **€1.50M in Profit**, and **10K Orders**, with **Tennis** as the leading product category, **Online** as the dominant sales channel, and **France** as the strongest geographic market. Overall **Sales YoY Growth is +49%**.

The dashboard is designed to move from **what happened → where it happened → what is driving it → where to investigate next**.

---

## 📊 Dashboard

!screenshots/dashboard.png

---

## 🎯 Business Questions

The dashboard was designed to answer:

- How much revenue and profit are being generated?
- How are sales trending over time?
- How does current sales performance compare with the previous year?
- Which product categories generate the most sales?
- Which countries and cities contribute most to sales?
- Which sales channels are driving revenue?

---

## 💡 Executive KPI Snapshot

| KPI | Result |
|---|---:|
| **Total Sales** | **€3.81M** |
| **Total Profit** | **€1.50M** |
| **Total Orders** | **10K** |
| **YoY Growth** | **+49%** |

---

# 🔎 Key Insights

### 🏆 Tennis leads category sales

**Tennis** is the strongest category at approximately **€0.57M**, followed by **Fitness (€0.55M)** and **Hiking & Camping (€0.53M)**.

**What this means:** these categories are important revenue drivers and should be monitored closely for assortment, inventory availability, pricing, and promotional opportunities.

### 🛒 Online is the dominant channel

**Online** contributes approximately **€1.71M**, followed by **Mobile App (€0.96M)** and **Click & Collect (€0.77M)**.

**What this means:** digital commerce is the primary revenue engine in the dataset, making the online customer journey an important area for optimization.

### 🌍 France is the strongest market

**France** generates approximately **€0.97M**, followed by **Spain (€0.62M)** and **Germany (€0.59M)**.

**What this means:** France is the strongest market in the dataset, while Spain and Germany provide additional opportunities for regional growth analysis.

### 📈 Sales are growing year over year

The monthly trend compares current sales with the previous year, with overall **Sales YoY Growth of +49%**.

**What this means:** the business is showing strong year-over-year momentum, while the monthly comparison helps identify changes in seasonal performance.

---

# 🚀 Business Recommendations

### 1. Prioritize high-performing categories

Focus on Tennis, Fitness, and Hiking & Camping when reviewing:

- Inventory availability
- Product assortment
- Pricing
- Promotional campaigns

### 2. Continue investing in digital channels

Online is the largest revenue contributor. The next analytical step should investigate the drivers behind this performance, including:

- Conversion rate
- Average order value
- Customer acquisition
- Mobile vs. desktop behavior
- Checkout abandonment

### 3. Evaluate channel profitability

Revenue leadership does not automatically mean profitability leadership.

A deeper channel analysis should compare:

**Sales → Profit → Profit Margin → Orders**

This would identify which channels create the most valuable revenue rather than simply the most revenue.

### 4. Investigate geographic opportunities

France is the strongest market, with Spain and Germany also contributing significantly.

Further analysis could compare:

- Sales per customer
- Profit margin by country
- Average order value
- Customer retention
- Category preferences by market

---

# 🎨 Dashboard Design

The final dashboard uses four complementary analytical views:

1. **Sales Trend** — monthly sales performance and previous-year comparison
2. **Category Performance** — sales contribution by product category
3. **Geographic Performance** — sales distribution across countries and cities using a treemap
4. **Channel Performance** — revenue contribution by e-commerce channel

Each visual was selected to answer a distinct business question. An earlier version contained two similar category-ranking visuals; the final design replaced the duplicate view with geographic analysis to improve analytical coverage.

---

# 🧩 Data Model

The project uses a **star-schema data model** with `tbl_Sales` as the central fact table and supporting dimension tables.

```text
                         Date
                          │
                          │
Customer ──────────── tbl_Sales ──────────── tbl_Product
                          │
                          │
                       Channel
                          │
                          │
                    tbl_Promotion
```

### Fact Table — `tbl_Sales`

Transaction-level information including:

- Order ID
- Customer Key
- Product Key
- Channel Key
- Promotion Key
- Order Date
- Quantity
- Unit Price
- Net Sales
- Profit

### Dimension Tables

- **Date**
- **Customer**
- **tbl_Product**
- **Channel**
- **tbl_Promotion**

The star schema supports consistent filtering, reusable DAX measures, and time-intelligence analysis across the report.

---

# 🧠 DAX Analysis

### Total Sales

```DAX
Total Sales =
SUM(tbl_Sales[NetSales])
```

### Total Orders

```DAX
Total Orders =
DISTINCTCOUNT(tbl_Sales[OrderID])
```

### Sales LY

```DAX
Sales LY =
CALCULATE(
    [Total Sales],
    SAMEPERIODLASTYEAR('Date'[Date])
)
```

### Sales YoY %

```DAX
Sales YoY % =
DIVIDE(
    [Total Sales] - [Sales LY],
    [Sales LY]
)
```

### Sales % of Total

```DAX
Sales % of Total =
DIVIDE(
    [Total Sales],
    CALCULATE(
        [Total Sales],
        REMOVEFILTERS(Channel)
    )
)
```

### High Value Product Sales

```DAX
High Value Product Sales =
CALCULATE(
    [Total Sales],
    FILTER(
        tbl_Sales,
        tbl_Sales[UnitPrice] > 100
    )
)
```

---

# 🛠️ Tools & Skills

### Tools

- **Power BI Desktop**
- **DAX**
- **Microsoft Excel**

### Skills Demonstrated

- Data preparation
- Star-schema data modeling
- Fact and dimension table design
- Relationship management
- KPI development
- DAX measure development
- Time intelligence
- Year-over-year analysis
- Product and category analysis
- Geographic analysis
- Channel analysis
- Dashboard UX
- Data storytelling
- Business recommendations

---

# 🔄 Project Workflow

```text
Structured Data
      ↓
Data Preparation
      ↓
Star-Schema Model
      ↓
Relationships
      ↓
DAX Measures
      ↓
KPI Development
      ↓
Visual Analysis
      ↓
Executive Dashboard
      ↓
Business Insights
      ↓
Recommendations
```

---

# 📦 Repository Contents

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
├── screenshots/
│   └── dashboard.png
│
└── docs/
    ├── dax-measures.md
    ├── data-model.md
    ├── business-insights.md
    └── project-story.md
```

---

# ▶️ How to Use

1. Download or clone the repository.
2. Open `powerbi/Decathlon_Ecommerce_Performance.pbix` in **Power BI Desktop**.
3. Review the dashboard and report interactions.
4. Open **Model view** to inspect the star-schema relationships.
5. Open **Data view** to explore the underlying tables.
6. Open the **Modeling** pane to review the DAX measures.
7. If the Excel source file is moved, update the source path in Power BI.

---

# 📚 What This Project Demonstrates

This project demonstrates my ability to turn structured business data into an executive BI solution.

The focus is not simply on creating visuals, but on connecting:

**Data → Model → Measures → Analysis → Insights → Decisions**

---

# ⚠️ Data Note

This is a **portfolio/practice analytics project** created for learning and demonstration purposes.

The dataset and results should **not** be interpreted as Decathlon's actual public financial reporting or internal company data.

---

# 👤 Author

**Semehar Hailu**  
Business Intelligence Engineer & Data Scientist

[LinkedIn](https://www.linkedin.com/in/semehar-mebrahtu-hailu-1a305519/) • [GitHub](https://github.com/Semehar1) • semeharhailu@gmail.com
