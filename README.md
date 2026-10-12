# Healthcare Data Analysis and Insights (Excel Dashboard)

An end-to-end Excel project that takes three raw healthcare tables, cleans and transforms them, and turns them into an interactive dashboard on patient health, hospitalisation and treatment costs.

![Healthcare dashboard](DashBoardCreated.PNG)

## Project Overview

Healthcare providers and policymakers need to know who their patients are, what conditions drive costs, and where money is being spent. This project works through a healthcare dataset covering **2,335 patients** and answers those questions using only Excel: formulas for cleaning and transformation, lookups to combine tables, pivot tables for analysis, and pivot charts with slicers for the dashboard.

It was completed as a module-end assignment, and the original brief is included in the repository.

## Objectives

- Clean the data by finding and fixing missing values (marked with `?`) and inconsistent text.
- Transform raw columns into analysis-ready fields (weight status, diabetes status, date of birth, age).
- Combine three tables into a single analysis sheet.
- Analyse health metrics and healthcare charges using pivot tables and charts.
- Build an interactive dashboard with slicers for **Weight Status** and **Diabetes Status**.

## Dataset

The data comes in three linked tables, joined on `Customer ID`:

| Table | What it holds |
|---|---|
| **Customer Names** | Customer ID and full name |
| **Medical Examinations** | BMI, HbA1c, heart issues, transplants, cancer history, major surgeries, smoker |
| **Hospitalisation Details** | Birth year / month / date, charges, hospital tier, city tier, state ID |

Dataset reference date: **8 June 2023** (used to calculate age).

## Workflow

### 1. Data cleaning
| Task | Approach |
|---|---|
| Find missing values marked `?` | Counted with pivot tables and highlighted with conditional formatting |
| Missing `month` / `year` | Month filled with **Sep**; year filled with the **average year, rounded** |
| Missing `smoker`, `Hospital tier`, `City tier` | Filled with the **most frequent value** (found via pivot tables): smoker = *No*, hospital tier = *tier - 2*, city tier = *tier - 2* |
| Missing `State ID` | Filled with **Unknown** |

Cleaned values are kept in new `Updated` columns beside the original data, so the raw values are never overwritten.

### 2. Data transformation
| Task | Approach |
|---|---|
| Split `name` into Title, First Name, Last Name | Flash Fill |
| `NumberOfMajorSurgeries` to numbers | Non-numeric entries such as "No major surgery" replaced with `0` |
| Fix inconsistencies in `Heart Issues`, `smoker`, `Any Transplants` | `PROPER()` to standardise text case |
| **Weight Status** from BMI | Below 18.5 Underweight, 18.5-24.9 Normal Weight, 25-29.9 Overweight, 30+ Obesity |
| **Diabetes Status** from HbA1c | Below 5.7 Normal, 5.7-6.4 Prediabetes, 6.5+ Diabetes |
| **Date of Birth** | Year, month and date merged and formatted as `DD-MMM-YYYY` |
| **Age** | `DATEDIF` between date of birth and 8 June 2023 |
| `charges` | Formatted as currency ($) |

### 3. Combining the tables
A new **HealthCare** sheet pulls everything together using lookup formulas on `Customer ID`, keeping the 17 columns needed for analysis (Customer ID, First Name, BMI, HbA1c, Heart Issues, Any Transplants, Cancer History, Major Surgeries, Smoker, Weight Status, Diabetes Status, Age, Date of Birth, Charges, Hospital tier, City tier, State ID).

### 4. Analysis and visualisation
Seven pivot tables on the **HealthCare_Analysis** sheet feed seven charts:

| Question | Chart |
|---|---|
| Cancer history among smokers and non-smokers | Pie |
| Major surgeries and average HbA1c with vs without transplants | Pie (x2) |
| Charges by weight status and diabetes status | Clustered column |
| Average charges by hospital tier across states | Clustered column |
| Age vs BMI and HbA1c | Line |
| Age vs healthcare charges | Line |

## Dashboard

The **Dashboard** sheet brings all charts together with three KPI cards and slicers that filter every chart at once.

- **KPIs:** 2,335 patients | $13,529.92 average charges | 30.97 average BMI
- **Slicers:** Weight Status, Diabetes Status (as required) and Smoker (added for extra comparison)

## Key Insights

- **Diabetes raises costs at every weight level.** Within each weight group, patients with diabetes have the highest average charges. The highest overall is obesity combined with diabetes, at about **$19,100**, compared with about **$7,400** for underweight patients with diabetes.
- **Weight and cost move together.** Obesity shows the highest charges across all three diabetes categories.
- **Charges rise with age.** Average charges climb from roughly **$6,500 at age 18** to roughly **$29,000 at age 64**, with some ups and downs along the way.
- **Tier-1 hospitals are generally the most expensive.** In most states, tier-1 hospitals have the highest average charges, while tier-2 and tier-3 are lower.
- **Cancer history:** 391 of 2,335 patients (**17%**) have a history of cancer.
- **Transplants:** Patients with a transplant history account for 162 of the 1,579 recorded major surgeries (**10%**) and show a noticeably lower average HbA1c (**5.19** vs **6.67**).

## Repository Contents

| File | Description |
|---|---|
| `Healthcare_Solved.xlsx` | Complete workbook: raw tables, cleaned columns, HealthCare sheet, pivot tables and dashboard |
| `DashBoardCreated.PNG` | Screenshot of the final dashboard |
| `Module End Assignment 1_Excel - Healthcare Analysis and Insights.pdf` | Original assignment brief |

### Workbook sheets
`Customer Names` | `Medical Examinations` | `Hospitalisation Details` | `SolutionS` (step-by-step answers) | `HealthCare` (combined data) | `HealthCare_Analysis` (pivot tables and charts) | `Dashboard`

## How to Use

1. Download `Healthcare_Solved.xlsx` and open it in Microsoft Excel (a recent desktop version is recommended, because the slicers and some formulas need it).
2. Go to the **Dashboard** sheet.
3. Click the **Weight Status**, **Diabetes Status** or **Smoker** slicers to filter all charts together. Click the filter-clear icon on a slicer to reset it.
4. Open **SolutionS** to see how each cleaning and transformation step was answered.

## Skills Demonstrated

- Data cleaning and validation in Excel (`IF`, `PROPER`, conditional formatting, Flash Fill)
- Date handling (`CONCAT`, `DATEDIF`, custom date formats)
- Combining tables with lookup formulas
- Pivot tables, pivot charts and slicers
- Dashboard design and data storytelling

## Limitations and Future Improvements

- The **Age vs BMI and HbA1c** chart plots *sums*, so it follows the number of patients at each age rather than showing a true relationship. Using *averages* or a `CORREL` calculation would give a clearer answer.
- Pie charts compare groups of very different sizes (for example 1,417 vs 162 surgeries), so rates per patient would be fairer than totals.
- The hospital-tier chart covers many states at once, which makes it busy. A state slicer would make it easier to read.
- Next steps: add statistical checks on the age-charges trend, and rebuild the dashboard in Power BI for easier sharing.

## Author

**Aiswarya R Nair**
