# E-commerce Sales Analysis (Excel)

An end-to-end Excel project: building a single analysis table from four related tables, cleaning it, and analysing 2,000 orders to find what drives revenue.

**Period covered:** 14 Oct 2023 – 13 Oct 2025 · **Orders:** 2,000 · **Customers:** 492 · **Products:** 100 · **Stores:** 20

---

## Contents

- [Project overview](#project-overview)
- [Repository structure](#repository-structure)
- [Data model](#data-model)
- [Data cleaning](#data-cleaning)
- [Key findings](#key-findings)
- [Recommendations](#recommendations)
- [Limitations](#limitations)
- [Tools used](#tools-used)
- [How to use this project](#how-to-use-this-project)
- [Author](#author)

---

## Project overview

The goal is to understand sales performance across categories, store types, regions, customer segments and discount levels, and to turn the findings into practical business recommendations.

The workflow:

1. Combine four source tables into one analysis table (`Project_DB`).
2. Audit and clean the data.
3. Summarise it with pivot tables and descriptive statistics.
4. Present the results in a dashboard, a PDF report and a one-page summary.

## Repository structure

```
├── mini_PROJECT.xlsx                              # Workbook: source tables, cleaned data, pivots, dashboard
├── Project_DB_Cleaning_and_Analysis_Report.pdf    # Cleaning steps (before/after snapshots) + full analysis
├── Project_DB_One_Page_Summary.docx               # One-page summary of findings and decisions
└── README.md
```

### Workbook sheets (`mini_PROJECT.xlsx`)

| Sheet | Purpose |
|---|---|
| `Customer_Dim` | Customer details: age, gender, location, loyalty level (500 rows) |
| `Product_Dim` | Product name, category, sub-category, brand, cost, stock (100 rows) |
| `Store_Dim` | Store name, region, city, store type (20 rows) |
| `Sales_Fact` | One row per order: date, IDs, quantity, price, discount, payment type, total (2,000 rows) |
| `Project_DB` | Joined analysis table (2,000 rows × 20 columns) |
| `Descriptive Analysis` | Summary statistics for the pivot outputs |
| `Pivot Table` | Pivot tables with written insights |
| `E-commerce Dashboard` | Dashboard with slicers |

## Data model

The workbook follows a star schema: `Sales_Fact` links to three dimension tables.

```
Customer_Dim ──(Customer_ID)──┐
Product_Dim  ──(Product_ID)───┼── Sales_Fact ──► Project_DB (joined table used for analysis)
Store_Dim    ──(Store_ID)─────┘
```

## Data cleaning

All checks were run on `Project_DB`. Every fix was validated against the source sheets.

| Issue | Rows | Decision |
|---|---|---|
| Header typo "Coustomer Name" | 1 column | Renamed to "Customer Name" |
| Country written as `USA`, `usa`, `UnitedStatesofAmerica` | 16 | Standardised to `USA` |
| Discount above 100% (3.84, 3.48, 1.66) | 3 | Rebuilt from `Total_Amount ÷ (Quantity × Unit_Price)` → 4%, 13%, 17% |
| Quantity stored as `2.9999999999999996` | 2 | Rounded to 3; column set to whole numbers |
| Text "Unknown" in numeric `Stock` | 57 (3 products) | Set to blank; excluded from stock calculations, kept in sales |
| "Unknown" loyalty level | 16 (4 customers) | Kept as its own group; excluded from tier comparisons |
| Duplicates, ID mismatches, total ≠ Qty × Price × (1 − Discount) | 0 after fixes | None remaining |

Columns added for analysis: `Region`, `Year`, `Month`, `Age_Group`, `Gross_Amount`, `Discount_Amount`.

Total revenue is unchanged by cleaning (₹21,74,394.70).

## Key findings

- **Sales are flat.** Revenue is ₹21.74 lakh with an average order value of ₹1,087. It runs at about ₹91K a month, and the second year is only 1.9% above the first.
- **Online is the largest channel** (42.0% of revenue). The **West** region has only 2 stores but the highest revenue per store (₹1.35L vs ₹1.04–1.08L elsewhere). STORE8 (Online, West) is the top store at ₹1.59L.
- **Sports (24.9%) and Electronics (23.2%)** drive the business. Beauty is the weakest category (14.8%) and holds the three lowest-revenue products. Clothing has the highest order value (₹1,135).
- **Female customers generate 56.6% of revenue**, with more orders per customer (4.2 vs 3.9) and a higher order value (₹1,124 vs ₹1,043).
- **Loyalty tier and age do not change spending.** Average order value is ₹1,073–₹1,104 across all tiers, so the loyalty programme is not yet driving bigger baskets.
- **Deep discounts do not buy volume.** Discounts total ₹3.82L (14.9% of gross sales). Offers of 21–30% account for 53% of that value, yet those orders contain no more units than orders with 0–10% off (2.47 vs 2.45).
- **The customer base is loyal:** 92% of customers ordered more than once.

## Recommendations

1. Cap discounts at about 20% and pilot the change in a few stores first.
2. Study STORE8 and consider more West-region stores; prioritise Sports and Electronics.
3. Review Beauty range, pricing and promotion.
4. Redesign loyalty rewards around basket size or purchase frequency.
5. Investigate the weak months (May 2024 and June 2025) and improve data capture (validate discounts, standardise country, record cost and stock for every product).

## Limitations

- `Unit_Price` varies widely for the same product, and cost is not held in `Project_DB`, so **margin and profit were not analysed**. All findings are on revenue.
- The first and last months of the data are partial.
- The three corrected discounts assume `Total_Amount` is accurate.
- Some segments are small
