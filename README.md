# Business Financial Performance Analysis

**Power BI Dashboard \| FY 2023**

An interactive, two-page financial dashboard analysing revenue,
expenses, profitability and financial efficiency across three business
lines.

## 1. Project Overview

This project uses Power BI to examine the financial performance of a
business across Sportswear, Sports equipment, and Nutrition and Food
Supplements.

The dashboard helps management compare business-line profitability,
understand the expense structure, monitor monthly financial movements
and identify areas requiring further investigation.

The report contains two pages:

1.  **Business Financial Performance** --- an overview of revenue,
    expenses, profit and business-line margins.
2.  **Expense and Efficiency Analysis** --- an examination of expense
    subgroups and expense-to-revenue ratios.

## 2. Business Questions

The analysis addresses four questions:

1.  Which business lines generate the strongest margin?
2.  How do expense subgroups trend across months and years?
3.  Which revenue-to-expense ratios have moved most over the series?
4.  How do seasonal patterns differ across lines of business?

**Scope limitation:** The dataset covers January--December 2023 only.
Monthly movements and business-line differences can be analysed, but
year-over-year trends and recurring seasonal patterns cannot be
established without additional years of data.

## 3. Dataset

The source is a CSV business financial dataset containing **580 records
and nine fields**.

  Field                       Description
  --------------------------- ------------------------------------
  `Year`                      Financial year
  `Month - name`              Month name
  `Month -sequence`           Numeric month sequence
  `Date`                      Reporting date
  `Business Line`             Business-line category
  `Amount, $`                 Signed financial amount in dollars
  `Expense subgroup`          Expense category, where applicable
  `Revenue / Expense Group`   Revenue or expense grouping
  `Revenue or expense`        Transaction classification

Revenue amounts are positive and expense amounts are negative in the
source data. The original signs were retained; DAX measures convert
expenses to positive values for expense reporting.

## 4. Tools and Techniques

-   **Power BI Desktop** --- data modelling, DAX measures, report design
    and interactive visualisation.
-   **Power Query** --- data cleaning, standardisation and data-type
    checks.
-   **DAX** --- financial KPIs, ratios and time-based measures.
-   **CSV** --- source data format.

Key preparation and modelling steps:

-   Trimmed and cleaned business-line text values to standardise
    categories.
-   Checked data types and converted the date field to a valid Date
    type.
-   Reviewed blank expense-subgroup values rather than automatically
    deleting them.
-   Preserved original signed financial amounts.
-   Created a dedicated Date table.
-   Created an active one-to-many relationship from `DateTable[Date]` to
    `FinancialData[Date]`.
-   Sorted month names by month number to preserve chronological order.

## 5. Key Performance Indicators

  ------------------------------------------------------------------------
  KPI                   Definition                      Full-period result
  --------------------- --------------------- ----------------------------
  Total Revenue         Sum of revenue                    **\$17,559,820**
                        transactions          

  Total Expenses        Absolute value of                 **\$13,245,700**
                        expense transactions  

  Net Profit            Total Revenue − Total              **\$4,314,120**
                        Expenses              

  Profit Margin         Net Profit ÷ Total                      **24.57%**
                        Revenue               

  Expense-to-Revenue    Total Expenses ÷                        **75.43%**
  Ratio                 Total Revenue         

  Revenue-to-Expense    Total Revenue ÷ Total                    **1.33x**
  Ratio                 Expenses              
  ------------------------------------------------------------------------

The expense-to-revenue ratio shows the share of revenue consumed by
recorded expenses. The revenue-to-expense ratio shows the revenue
generated per dollar of recorded expense.

### Core DAX measures

``` dax
Total Revenue =
CALCULATE(
    SUM(FinancialData[Amount, $]),
    FinancialData[Revenue or expense] = "Revenue"
)
```

``` dax
Total Expenses =
-CALCULATE(
    SUM(FinancialData[Amount, $]),
    FinancialData[Revenue or expense] = "Expense"
)
```

``` dax
Net Profit =
[Total Revenue] - [Total Expenses]
```

``` dax
Profit Margin =
DIVIDE([Net Profit], [Total Revenue])
```

``` dax
Expense-to-Revenue Ratio =
DIVIDE([Total Expenses], [Total Revenue])
```

``` dax
Revenue-to-Expense Ratio =
DIVIDE([Total Revenue], [Total Expenses])
```

## 6. Dashboard Pages

### Page 1 --- Business Financial Performance

**KPIs** - Total Revenue - Total Expenses - Net Profit - Profit Margin

**Visualisations** - Profit margin by business line (horizontal bar
chart). - Revenue versus expenses by business line (clustered column
chart). - Monthly revenue performance (area/line chart).

**Purpose:** Compare business-line profitability and scale, and review
monthly revenue movements.

### Page 2 --- Expense and Efficiency Analysis

**Visualisations** - Expense breakdown by subgroup (horizontal bar
chart). - Monthly expense distribution by subgroup (matrix with
conditional formatting). - Monthly expense-to-revenue ratio (line
chart). - Monthly expense-to-revenue ratio by business line
(multi-series line chart).

**Purpose:** Identify major expense categories, inspect monthly expense
distributions and compare the proportion of revenue consumed by expenses
across business lines.

### Interactivity

The report includes synchronised slicers for **Business Line** and
**Date**. KPI cards and relevant visuals respond to the selected filter
context. A page navigator provides movement between the two report
pages.

## 7. Key Findings

### 7.1 Sportswear has the strongest profit margin

  Measure            Sportswear
  --------------- -------------
  Revenue           \$6,807,700
  Expenses          \$4,070,900
  Net profit        \$2,736,800
  Profit margin      **40.20%**

Sportswear has the highest profit margin among the three business lines.

### 7.2 Sports equipment generates the highest revenue

  Measure           Sports equipment
  --------------- ------------------
  Revenue                \$8,908,500
  Expenses               \$6,618,300
  Net profit             \$2,290,200
  Profit margin           **25.71%**

Sports equipment is the largest revenue contributor, but its margin is
lower than Sportswear's. The business line with the highest revenue is
not necessarily the one with the strongest margin.

### 7.3 Nutrition and Food Supplements is loss-making

  Measure           Nutrition and Food Supplements
  --------------- --------------------------------
  Revenue                              \$1,843,620
  Expenses                             \$2,556,500
  Net profit                        **-\$712,880**
  Profit margin                        **-38.67%**

Recorded expenses exceed revenue for this business line. It should be
prioritised for a more detailed profitability review.

### 7.4 Labor is the largest expense subgroup

Labor expenses total approximately **\$4,492,000**, making Labor the
largest expense subgroup. Payroll is approximately **\$1,790,000**.

Labor and Payroll together account for approximately 47.4% of total
recorded expenses. Their accounting definitions should be checked to
confirm that they represent distinct, non-overlapping cost categories.

### 7.5 Expense efficiency varies by month

The monthly expense-to-revenue ratio changes across 2023. This indicates
that the proportion of revenue consumed by recorded expenses was not
constant throughout the year.

The ratio alone does not explain the cause of a movement. Revenue and
expense amounts should be examined together to determine whether a
change is driven by higher expenses, lower revenue or both.

## 8. Recommendations

1.  **Investigate Nutrition and Food Supplements:** Review pricing,
    product mix, sales volumes and cost allocation to understand the
    causes of its negative result.
2.  **Understand Sportswear's margin advantage:** Examine pricing,
    product mix and cost drivers to identify practices that may be
    transferable to other business lines.
3.  **Review Sports equipment cost efficiency:** Investigate the factors
    behind its lower margin relative to Sportswear, while protecting
    revenue and product quality.
4.  **Monitor labor-related costs:** Analyse labor expenditure alongside
    staffing levels, productivity and business activity. A high expense
    is not automatically an avoidable expense.
5.  **Monitor monthly expense efficiency:** Investigate months with
    higher expense-to-revenue ratios by reviewing the underlying revenue
    and expense movements.

These are investigation priorities, not proof of the underlying causes.
The dataset identifies where management should look; additional
operational and accounting information is needed to confirm why the
results occurred.

## 9. Limitations and Assumptions

-   **One year of data:** Only 2023 is available. Year-over-year
    comparisons and recurring seasonality cannot be established.
-   **Recorded expenses:** Profit measures reflect only revenue and
    expense records included in this dataset. They should not
    automatically be interpreted as statutory net income or operating
    profit without confirming the completeness and accounting
    classification of the source data.
-   **Expense subgroup blanks:** Blank subgroup values require
    interpretation in context. Revenue records may legitimately have no
    expense subgroup; expense records with missing subgroup
    classifications should be investigated.
-   **Expense categories:** The definitions of Labor and Payroll should
    be checked to confirm that they are distinct and non-overlapping.
-   **Business interpretation:** The dashboard identifies patterns and
    differences but does not, by itself, establish causation.

## 10. Repository Contents

Suggested repository structure:

``` text
business-financial-performance/
├── README.md
├── Business_Financial_Performance.pbix
├── data/
│   └── Business Financial Dataset.csv
└── screenshots/
    ├── financial-performance.png
    └── expense-efficiency-analysis.png
```

Only include the source dataset in a public repository if you have
permission to share it. If the data is confidential or licensed, omit it
and document how users can obtain an authorised copy.

Replace the example PBIX and screenshot filenames above with the actual
filenames used in your repository.

## 11. Conclusion

This project demonstrates how Power BI can transform financial records
into an interactive management report. By combining data preparation,
data modelling, DAX measures and business-focused visualisations, the
dashboard highlights differences in business-line profitability, major
expense categories and monthly financial efficiency.

The analysis identifies Sportswear as the strongest business line by
profit margin, Sports equipment as the largest revenue contributor and
Nutrition and Food Supplements as a loss-making line requiring further
investigation.

------------------------------------------------------------------------

**Project type:** Financial Performance Analysis\
**Reporting period:** January--December 2023\
**Visualisation tool:** Microsoft Power BI Desktop\
**Pages:** 2
