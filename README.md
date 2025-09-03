# Power-BI

# COGS Optimization Dashboard

### Purpose
Compare SKU version costs (v1 vs v2) and calculate savings $ / %.

### Visuals
- KPI Cards: Cost v1, Cost v2, Savings $, Savings %
- Column Chart: COGS by version (per SKU)
- Treemap (optional): Ingredient contribution

### DAX
```DAX
Cost v1 = CALCULATE(SUM(bom_costs[bom_cost]), bom_costs[version_no] = 1)
Cost v2 = CALCULATE(SUM(bom_costs[bom_cost]), bom_costs[version_no] = 2)
Savings $ = [Cost v1] - [Cost v2]
Savings % = DIVIDE([Savings $], [Cost v1])


---

## Vendor Comparison Dashboard

### Purpose
Compare Vendor Alpha vs Vendor Beta pricing and show savings if switching.

### Visuals
- Bar Chart: Ingredient vs Avg Price by Vendor
- KPI: Savings if Switch %
- Line Chart: Price trends (X=Date, Y=Price, Legend=Vendor)

### DAX
```DAX
Avg Price = AVERAGE(price_trends[price_per_uom])
Alpha Price = CALCULATE([Avg Price], price_trends[vendor_name] = "Vendor Alpha")
Beta Price  = CALCULATE([Avg Price], price_trends[vendor_name] = "Vendor Beta")
Savings if Switch % = DIVIDE([Alpha Price] - [Beta Price], [Alpha Price])


---

## Ingredient Price Trends Dashboard

### Purpose
Show monthly price trends by vendor for each ingredient.

### Visuals
- Line Chart:
  - X-axis = price_date (Date, Continuous)
  - Y-axis = price_per_uom (Avg or Don’t Summarize)
  - Legend = vendor_name
- Slicer: ingredient_name

## NMPA Submission Readiness Dashboard

### Purpose
Track readiness of products for Annex 14 submission and monitor data quality.

### Visuals
- KPI Cards: Total Products, Ready, Pending Validation, Blocked, Ready %
- Stacked Bar: submission_status by count
- Table: product_name, completeness_pct, compliance_flag, target_submission_date
- Slicers: brand, region

### DAX
```DAX
Total Products = DISTINCTCOUNT(products[product_id])
Ready Products = CALCULATE(DISTINCTCOUNT(products[product_id]), products[submission_status] = "Ready")
Pending Validation = CALCULATE(DISTINCTCOUNT(products[product_id]), products[submission_status] = "Pending Validation")
Blocked Products = CALCULATE(DISTINCTCOUNT(products[product_id]), products[submission_status] = "Blocked")
Ready % = DIVIDE([Ready Products], [Total Products])



