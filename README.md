# Shopify App Store Analysis

## Analyst Memo — Shopify App Store Insights

**Dashboard:** Shopify App Store Analysis  
**Reporting Period:** Latest available data

### Key Insight

The Shopify App Store dataset contains **500 apps** and **7,980 customer reviews**. The overall **average rating is 4.19 out of 5**, indicating generally positive merchant satisfaction. However, the **developer reply rate is 24.8%**, meaning that fewer than one in four reviews received a recorded developer response. The dashboard also provides category and time-based views to identify differences in review activity and marketplace performance.

### Business Impact

The strong overall rating suggests that merchants are generally satisfied with the available apps, but the relatively low developer response rate represents an opportunity to strengthen communication between developers and merchants. Developer engagement can help merchants feel heard, clarify concerns, and improve the quality of the marketplace experience. Category-level and time-based analysis can also help Shopify identify areas with stronger engagement and areas that may require additional attention.

### Recommendation

Shopify should encourage app developers to increase their response rates, particularly for lower-rated or negative reviews. Marketplace teams should use the category and trend analysis in this dashboard to identify categories with unusually high or low review activity and monitor changes over time. These insights can support targeted developer education, marketplace quality initiatives, and ongoing monitoring of merchant satisfaction.

---

## Project Overview

This project analyzes Shopify App Store applications and customer reviews using **Power BI**. The objective is to understand app popularity, merchant satisfaction, developer engagement, category performance, and review trends over time.

The report contains two main pages:

1. **Overview** — Provides a high-level marketplace summary using KPI cards, slicers, and category/time-based visuals.
2. **Trend Analysis** — Applies time-intelligence calculations to analyze review activity, period comparisons, and accumulated metrics.

---

## Dataset

The analysis uses two CSV files:

- `apps.csv` — Contains one row per Shopify app, including app name, developer, category, launch date, pricing model, and free-plan availability.
- `reviews.csv` — Contains customer review information, including rating, review date, developer response, and helpful votes.

### Main fields

**apps.csv**
- `app_id`
- `app_name`
- `developer`
- `category_name`
- `launch_date`
- `has_free_plan`
- `monthly_price_usd`

**reviews.csv**
- `review_id`
- `app_id`
- `rating`
- `posted_at`
- `has_developer_reply`
- `helpful_count`

---

## Data Preparation

The raw data was cleaned in Power Query before analysis.

The following transformations were applied:

- Trimmed extra spaces from `app_name` and `developer`.
- Replaced missing developer names with `Unknown Developer`.
- Standardized `category_name` using Capitalize Each Word.
- Removed duplicate review records using `review_id`.
- Filtered review ratings to retain only values from 1 through 5.
- Converted `posted_at` using the appropriate locale so mixed date formats were interpreted correctly.
- Replaced `Yes` and `No` values in `has_developer_reply` with `1` and `0`.
- Reviewed and corrected column data types.

---

## Data Model

The Power BI model uses a star-schema structure:

```text
                 dim_date
                    |
                    |
apps  --------->  reviews
```

The relationships are designed so that:

- `apps[app_id]` connects to `reviews[app_id]`.
- `dim_date[Date]` connects to the review date field.
- `apps` acts as the application dimension.
- `reviews` provides review activity and customer feedback.
- `dim_date` supports time-based analysis and DAX time intelligence.

A dedicated calendar table named `dim_date` was created using DAX.

---

## Key Measures

The report includes measures for the major KPIs and time-intelligence analysis, including:

- **Total Apps**
- **Total Reviews**
- **Average Rating**
- **Developer Reply %**
- **Five Star Reviews**
- **Helpful Reviews**
- **Reviews MTD**
- **Reviews YTD**
- **Reviews Previous Year**
- **Review Growth %**
- **Cumulative Reviews**

These measures support the dashboard KPIs, trend visuals, and time comparisons.

---

## Dashboard Pages

### Overview

The Overview page provides a high-level view of marketplace performance.

It includes:

- Total Apps KPI
- Total Reviews KPI
- Average Rating KPI
- Developer Reply % KPI
- Category slicer
- Year slicer
- Has Free Plan slicer
- Reviews over time
- Reviews by category
- Page navigation

The layout follows a visual hierarchy intended to make the most important business metrics easy to identify first.

### Trend Analysis

The Trend Analysis page focuses on review activity over time.

It uses the `dim_date` calendar table and DAX time-intelligence functions such as:

- `CALCULATE()`
- `DATEADD()`
- `SAMEPERIODLASTYEAR()`
- `TOTALYTD()`
- `TOTALMTD()`

The page is designed to help stakeholders understand changes in review activity, compare periods, and evaluate cumulative performance.

---

## Repository Structure

```text
shopify-app-store-analysis/
├── README.md
├── report.pbix
├── data/
│   ├── apps.csv
│   └── reviews.csv
└── screenshots/
    ├── overview_page.png
    ├── trend_analysis_page.png
    └── model_view.png
```

---

## How to Use the Report

1. Open `report.pbix` using Power BI Desktop.
2. Confirm that the data sources are available if the report needs to be refreshed.
3. Use the **Overview** page for the marketplace summary.
4. Use the slicers to filter by category, year, and free-plan availability.
5. Navigate to **Trend Analysis** for time-based review analysis.
6. Refresh the report after replacing or updating the source datasets.

---

## Maintenance Notes

Future analysts should preserve the following model requirements:

- Keep `dim_date` as the dedicated calendar table.
- Maintain the relationship between `apps` and `reviews` through `app_id`.
- Maintain the date relationship required for time-intelligence measures.
- Apply data-cleaning transformations in Power Query rather than manually editing source data.
- Keep KPI and time-intelligence calculations as DAX measures so they respond dynamically to report filters.
- If the source data structure changes, review the Power Query steps and relationships before refreshing the report.

---

## Business Use

This dashboard can support Shopify marketplace teams in:

- Monitoring merchant satisfaction.
- Understanding review activity.
- Identifying high-engagement categories.
- Evaluating developer responsiveness.
- Monitoring changes in review activity over time.
- Supporting marketplace quality and developer-engagement initiatives.

---

## Deliverables

The completed project contains:

- Power BI report (`report.pbix`)
- Project documentation (`README.md`)
- Source datasets (`apps.csv` and `reviews.csv`)
- Overview screenshot (`overview_page.png`)
- Trend Analysis screenshot (`trend_analysis_page.png`)
- Data model screenshot (`model_view.png`)
