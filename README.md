# Vendor Performance & Procurement Intelligence Dashboard
**Power BI | DAX | Star Schema | Agri-Tech Domain**

> A 5-page multi-stakeholder Power BI dashboard built to solve a real procurement visibility problem in an agri-tech supply chain. Designed as a daily MIS tool for 5 different stakeholders — from co-founder to quality manager.

---

## The Problem This Solves

In agri-tech companies, procurement teams manage dozens of vendors across seeds, fertilizers, equipment, and packaging. Without a centralised view:

- No one knows which vendors are chronically late
- Spend overruns go undetected until month-end
- Quality rejection data sits in spreadsheets, unused
- Leadership makes vendor decisions based on gut feel

This dashboard puts all of that on one screen — updated in real time.

---

## Dashboard Pages

| Page | Primary User | Key Questions Answered |
|------|-------------|----------------------|
| **1. Executive Summary** | Co-Founder | What is our total spend? Are we on track? Any red flags? |
| **2. Vendor Scorecard** | Procurement Manager | Which vendors are reliable? Who should we review? |
| **3. Delivery & Operations** | Operations Head | Why are deliveries late? Which regions are worst? |
| **4. Spend & Budget** | Finance Controller | Where are we overspending? Which category is over budget? |
| **5. Quality Control** | Quality Manager | Which vendors have high rejection rates? Pass vs fail ratio? |

---

## Key Insights Found

After building the dashboard, the data revealed:

- **82% of deliveries were late** — only 78 out of 443 arrived on time
- **Equipment spend was 520% over budget** — highest overspend category
- **40% of quality inspections failed** — a systemic quality issue
- **KisanChem Industries** had only 4.76% on-time delivery rate — worst vendor
- **SafePack Ltd** had 47.37% on-time rate — most reliable vendor
- **137M budget variance** — company is significantly overspent on procurement

---

## Technical Skills Demonstrated

### Data Modeling
- Star schema with 5 tables and 5 relationships
- Dimension table: `Vendors`
- Fact tables: `Purchase_Orders`, `Deliveries`, `Quality_Inspection`, `Budget`
- Active and inactive relationships (inactive used with `USERELATIONSHIP()`)
- Dedicated `_Measures` table for professional DAX organisation

### DAX Measures Written

```dax
-- Safe division (avoids divide-by-zero errors)
On Time Delivery % = 
DIVIDE(
    COUNTROWS(FILTER(Deliveries, Deliveries[DeliveryStatus] = "On Time")),
    COUNTROWS(Deliveries)
) * 100

-- Filter context override
Delivered POs = 
CALCULATE(
    COUNTROWS(Purchase_Orders),
    Purchase_Orders[Status] = "Delivered"
)

-- Weighted rejection rate (more accurate than averaging percentages)
Avg Rejection Rate = 
DIVIDE(
    SUM(Quality_Inspection[UnitsRejected]),
    SUM(Quality_Inspection[TotalUnitsInspected])
) * 100
```

### Power Query
- Loaded 5 CSV files into Power Query Editor
- Verified date columns auto-detected as calendar type
- Applied data type checks before loading

### Visualisations Used
- KPI Cards, Donut Chart, Bar/Column Charts, Line Chart, Table, Stacked Bar
- Interactive slicers: Date Range (Between) + Category Dropdown
- Conditional formatting on vendor scorecard table

---

## Dataset

Synthetic agri-tech supply chain data generated for this project:

| Table | Rows | Description |
|-------|------|-------------|
| Vendors.csv | 25 | Vendor master with region, category, status |
| Purchase_Orders.csv | 600 | 18 months of PO data with value and status |
| Deliveries.csv | 443 | Expected vs actual delivery dates |
| Quality_Inspection.csv | 443 | Rejection rates and quality scores |
| Budget.csv | 90 | Monthly budget vs actual by category |

---

## Project Structure

```
vendor-procurement-dashboard/
│
├── data/
│   ├── Vendors.csv
│   ├── Purchase_Orders.csv
│   ├── Deliveries.csv
│   ├── Quality_Inspection.csv
│   └── Budget.csv
│
├── Vendor_Procurement_Dashboard_Sakshi_Idulganti.pbix
└── README.md
```

---

## How to Run

1. Clone or download this repository
2. Open `Vendor_Procurement_Dashboard_Sakshi_Idulganti.pbix` in Power BI Desktop
3. If prompted, update data source paths to point to the `/data` folder
4. Refresh the data — all 5 pages will load with live DAX calculations

---

## Author

**Sakshi Idulganti**  
Junior Consultant & Data Analyst | S4S Technologies  
[LinkedIn](https://linkedin.com/in/sakshiidulganti) • [GitHub](https://github.com/SSI06)  
idulgantisakshisantosh@gmail.com
