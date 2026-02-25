# Semantic Layer: Business Metrics Glossary

## Overview

This document defines all business metrics used across the organization. It serves as the **single source of truth** for metric definitions, ensuring consistency across all dashboards, reports, and analyses.

**Database**: Metabase Sample Database  
**Project**: E-Commerce Analytics  
**Last Updated**: February 25, 2026

---

## Core Metrics

### 1. Total Revenue

**Business Definition**:
Total monetary value of all orders, including discounts applied.

**Technical Formula**:
```sql
SUM(Orders.Total)
```

**Dimensions** (ways to slice this metric):
- Product Category
- Customer State/City
- Time (Year, Month, Day)
- Customer Segment

**Example Use Cases**:
- Monthly revenue trends
- Revenue by product category
- Revenue by region/state
- Year-over-year revenue comparison

**Notes**:
- Includes all completed and pending orders
- Discount amounts are already subtracted in the Total field

---

### 2. Order Count

**Business Definition**:
Total number of orders placed in the specified time period or dimension.

**Technical Formula**:
```sql
COUNT(DISTINCT Orders.ID)
```

**Dimensions** (ways to slice this metric):
- Product Category
- Customer State/City
- Time (Year, Month, Day)
- Customer Segment
- Payment Method

**Example Use Cases**:
- Transaction volume analysis
- Order trends by month
- Orders per region
- Order frequency by customer segment

**Notes**:
- Counts unique orders (not line items)
- Includes all order statuses

---

### 3. Average Order Value (AOV)

**Business Definition**:
Average monetary value per order. Used to track customer spending behavior and pricing effectiveness.

**Technical Formula**:
```sql
Total Revenue / Order Count
```

Or directly:
```sql
AVG(Orders.Total)
```

**Dimensions** (ways to slice this metric):
- Product Category
- Customer State/City
- Time (Year, Month, Day)
- Customer Segment
- Payment Method

**Example Use Cases**:
- Identify which product categories have highest AOV
- Track AOV trends over time
- Compare AOV across regions
- Measure impact of pricing changes
- Segment customers by spending patterns

**Benchmark**:
- General e-commerce AOV: $50-150
- Premium segments: $100+

---

## Dimensions (Classification Fields)

### Time Dimension
- **Year**: 2024, 2025, 2026
- **Month**: January through December
- **Quarter**: Q1, Q2, Q3, Q4
- **Day**: 1-31
- **Day of Week**: Monday through Sunday

**Usage**: Date range filtering, trend analysis

---

### Product Dimension
- **Category**: Gadget, Widget, Gizmo, Doohickey, etc.
- **Product Name**: Individual product names
- **Price Range**: Low ($0-50), Medium ($50-500), High ($500+)

**Usage**: Category-level analysis, product performance comparison

---

### Customer Dimension
- **State**: CA, NY, TX, etc. (US states)
- **City**: Customer city location
- **Country**: Customer country
- **Customer Segment**: VIP, Regular, New (derived from purchase history)

**Usage**: Geographic analysis, regional performance

---

## Key Insights from OLAP Operations

### Roll-up Example
"Total Revenue by Year" (aggregate upward)
```
2024: $850,000
2025: $920,000
2026: $345,000 (year-to-date)
```

### Drill-down Example
"Total Revenue by Month" (disaggregate downward)
```
2026-01: $115,000
2026-02: $230,000
...
```

### Slice Example
"Revenue from Gadget category only"
```
Filtered view showing only Gadget sales across all dimensions
```

### Dice Example
"Revenue from Gadgets in CA, by Month"
```
Multi-dimensional filter: Product=Gadget AND State=CA
Shows monthly revenue for this specific combination
```

---

## Governance & Best Practices

### Metric Consistency Rules
1. Always use the **officially defined formulas** above
2. Do not create ad-hoc variations (e.g., never use `SUM(Total * 1.1)` without approval)
3. When creating new metrics, document them in this glossary
4. All metrics should have clear business definitions, not just SQL

### When to Use Which Metric
- **Total Revenue**: Revenue forecasting, high-level business performance
- **Order Count**: Volume analysis, market penetration, growth rates
- **Average Order Value**: Pricing strategy, customer segment analysis, upsell opportunities

### Metric Relationships
```
Total Revenue = Order Count × Average Order Value
```
(This relationship should always hold true; if it doesn't, investigate data quality issues)

---

## Real-World Application

### Example Dashboard: Monthly E-Commerce Performance
```
Dashboard Layout:
├── Total Revenue (card showing month-to-date)
├── Order Count (card showing month-to-date)
├── Average Order Value (card showing month-to-date)
├── Revenue Trend (line chart: Revenue by month for past 12 months)
├── Orders by Category (bar chart: Order Count by Product Category)
├── Top Performing States (map showing Revenue by State)
└── Revenue by Region vs. Orders by Region (comparative analysis)
```

All metrics in this dashboard use the definitions above, ensuring consistency.

---

## FAQ

**Q: Why is "Total Revenue" different in my custom query?**  
A: Ensure you're using the official formula above. Check for any additional filters or exclusions in your query.

**Q: Can I modify these metric definitions?**  
A: No. To propose changes, contact the Data Governance team. Changes require approval and must be documented.

**Q: What if I need a metric that's not listed here?**  
A: Propose it to this document. All new metrics require business justification and technical validation.

---

## Related Concepts

- **OLAP Cube**: Pre-aggregated data structure that powers fast queries
- **Semantic Layer**: This document + Metabase metrics = your semantic layer
- **Star Schema**: The data model structure (Fact table + Dimension tables)
- **Pre-aggregation**: OLAP cubes pre-compute these metrics for instant query performance

---

## Version History

| Date | Author | Changes |
|------|--------|---------|
| 2026-02-25 | Learning Project | Initial metric definitions created |

