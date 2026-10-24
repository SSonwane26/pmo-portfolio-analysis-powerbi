# PMO Portfolio Analysis

> Analyzing monthly performance across 100 projects to help a PMO identify projects that may need recovery, review, acceleration, or data verification.

**Tools:** Excel | Power Query | Power BI | DAX  
**Project type:** Provided case-study dataset  
**Author:** Saurabh Sonwane  
**Full case study:** [Add link to the case study document]  
**Power BI report:** [Add published report or portfolio link]

---

## Dashboard Preview

![PMO Portfolio Analysis Dashboard](images/dashboard_preview.png)

> Replace `images/dashboard_preview.png` with a screenshot from your final report. Add the image to the repository at that path, or update the path above.

---

## Project Overview

A Project Management Office (PMO) helps an organisation plan, track and govern its projects. It reviews whether projects are on schedule, within budget, managing risks, using resources well, and expected to deliver their planned benefits.

In this case study, I analysed a provided project portfolio workbook and built a four-page Power BI report. The report brings delivery, financial, risk, resource and benefit indicators into one place. It also uses clear, rule-based checks to highlight projects that may need management attention.

The action labels are analytical suggestions based on this case study's rules. They are not automatic decisions or official company policy.

## Business Questions

1. Which projects are behind plan or forecast to be delayed?
2. Which projects have the largest forecast budget overruns?
3. Which projects have high risk exposure or overdue mitigation actions?
4. Which Business Units show the largest resource shortages?
5. Which projects have the largest benefit shortfalls?
6. Which projects may need recovery, a pause, acceleration, or data-freshness review?

## Dataset

- **Source:** A provided Excel case-study workbook: `PMO Portfolio_From Strategy to Success_C41.xlsx`
- **Main table:** `FactProjectMonthly`
- **Table grain:** One row per project per reporting date
- **Fact table size:** 1,696 monthly project records
- **Projects:** 100 unique projects
- **Reporting period in the fact data:** October 2023 to September 2026
- **Calendar dimension:** 1 January 2023 to 31 December 2026
- **Other tables:** Project, Programme, Business Unit, Employee, Location, Delivery Model, Strategic Theme and Date dimensions, plus a data dictionary
- **Current snapshot:** `CurrentProjectSnapshot`, a Power BI calculated table with one latest available record per project
- **Data sharing:** The source workbook is not included in this repository by default. Share it only if you have permission.

The latest available record for each project may not be from the same reporting date. Therefore, the current snapshot can include stale records and the report includes a data-freshness check.

## Approach

1. **Business understanding:** Defined questions around schedule, cost, risk, resources, benefits and portfolio decisions.
2. **Data exploration (Excel):** Reviewed workbook tables, fields, date coverage and the data dictionary.
3. **Data quality checks (Power Query / model checks):** Checked uniqueness of project-date records, dimension keys, key matches and selected milestone/risk logic.
4. **Data modelling (Power BI):** Built relationships between fact and dimension tables and created `CurrentProjectSnapshot`.
5. **Measures and decision rules (DAX):** Created measures for progress gap, forecast budget overrun, delay, risk, resource shortage and benefit shortfall. Added rule-based warning counts and recommended actions.
6. **Dashboard (Power BI):** Built four pages with KPI cards, charts, tables, slicers and report-page tooltips.
7. **Review and interpretation:** Compared the results with the business questions and documented data limitations.

**SQL was not used in this version of the project.** The work described here used Excel, Power Query, Power BI and DAX.

## Power BI Report Pages

### 1. PMO Portfolio Overview
- Total and Active project counts
- Average health score for Active projects
- Projects with outdated data
- Project status and monthly RAG trend
- Project count by Business Unit
- Ten weakest Active projects by health score

### 2. Delivery & Financial Performance
- Projects behind plan and projects with forecast delay
- Forecast budget overrun and overrun percentage
- Top projects by progress gap, forecast overrun and delay
- Project delivery and cost details
- Report-page tooltips for supporting measures

### 3. Risk, Resources & Benefits
- Critical risks and overdue mitigation actions
- Risk exposure by project
- Resource shortage hours by Business Unit
- Benefit shortfall by project
- Projects requiring attention
- Report-page tooltips for supporting measures

### 4. Portfolio Decisions
- Recommended-action KPI cards
- Strategic Alignment Score versus Portfolio Health scatter chart
- Recommended actions by Business Unit
- Projects requiring management attention
- Acceleration candidates for management review

## Key Findings

The following figures reflect the current case-study report and its measures. They should be checked against the final Power BI file before publishing.

- **100 projects** are included in the project-level snapshot. Latest available status: 55 Active, 40 Completed, 3 Terminated and 2 Paused.
- **61 projects** have a latest available record older than the portfolio's latest reporting date, 30 September 2026. This is a relative freshness check, not a claim that every record is more than 30 days old.
- **49 projects** are flagged as behind plan and **48 projects** have a forecast delay under the current report filters and definitions.
- Net forecast budget overrun is approximately **€12 million**, or **13.8% of baseline budget**, under the current report context.
- **42 projects** have critical risks, and the report shows **107 overdue mitigation actions**.
- Total resource shortage is approximately **34,000 hours**.
- Benefit shortfall to date is approximately **€34 million**; benefit realisation was approximately **72%** under the earlier KPI calculation.
- In the rule-based action output, 29 projects are marked Recover, 18 Review Data Freshness, 6 Accelerate, 4 Pause for Review, 43 No Further Intervention, and 0 Monitor.

### Important interpretation notes

- These are case-study results, not verified results from a named company.
- The current snapshot uses each project's latest available row, so reporting dates can differ between projects.
- The September 2026 monthly RAG chart contains 39 records: 34 Green and 5 Amber, with no Red records shown for that month. Do not confuse this monthly view with the 100-project latest-available snapshot.
- “No Further Intervention” applies to Completed or Terminated projects under the current rule order. It does not mean the project was successful.
- Recommendation counts depend on thresholds selected for this case study and require business review before real-world use.

## Recommendations

| Action | Projects | Reason / suggested next step |
|---|---:|---|
| Review Data Freshness | 18 | Confirm current status, forecast, risks, resources and benefits before relying on the older record. |
| Recover | 29 | At least one material warning signal is present. Agree a recovery plan with an owner, action, due date and target measure. |
| Pause for Review | 4 | A project is Paused or has three or more severe warning signals under the rule order. Review risk, dependencies, cost and business need. |
| Accelerate | 6 | Projects meet the initial acceleration rules. Confirm strategic priority and resource capacity before approving acceleration. |
| No Further Intervention | 43 | Projects are Completed or Terminated under the current rule order. Keep them out of active intervention queues while retaining relevant closure records. |
| Monitor | 0 | No projects fell into this category under the current thresholds and rule order. |
| Terminate | Not implemented | No automatic termination rule was implemented. Termination should not be recommended without agreed criteria and a wider business review. |

## Data Model and Measure Notes

- `FactProjectMonthly` is used for historical trends.
- `CurrentProjectSnapshot` is used for current project-level comparisons.
- Dimension tables support grouping and filtering by date, project, Business Unit, Programme and other descriptive fields.
- **Progress Gap (pp):** Average Actual Progress % minus Average Planned Progress %, multiplied by 100.
- **Forecast Budget Overrun (€):** Total Forecast Cost minus Total Baseline Budget. A positive result means forecast cost is above baseline.
- **Resource Shortage (hours):** The sum of the magnitude of negative resource capacity gaps, where available hours are lower than planned hours.
- **Benefit Shortfall to Date:** Planned Benefits Due to Date minus Benefits Realised to Date.
- The source `RiskExposureScore` is used as provided; its exact formula was not independently recreated.

## Folder Structure

Update this example to match the folders and files you actually publish:

```text
pmo-portfolio-analysis/
|-- powerbi/
|   |-- PMO_Portfolio_Analysis.pbix
|-- images/
|   |-- dashboard_preview.png
|   |-- page_1_overview.png
|   |-- page_2_delivery_financial.png
|   |-- page_3_risk_resources_benefits.png
|   |-- page_4_portfolio_decisions.png
|-- docs/
|   |-- PMO_Portfolio_Analysis_Case_Study.docx
|   |-- PMO_Portfolio_Analysis_Part_B_Career_Assets.docx
|-- README.md
```

> No SQL folder is listed because SQL scripts were not created for this version. Do not include the source workbook unless you have permission to redistribute it.

## How to Use This Project

1. Clone or download this repository.
2. Open the `.pbix` file in `powerbi/` using Power BI Desktop.
3. Use the Business Unit and Programme slicers to explore the report.
4. Review each report page, and hover over supported visuals to see report-page tooltips.
5. Read the case study in `docs/` for the business context, definitions, findings and limitations.

The source workbook is not included by default. If you have permission to share it, add it to the repository and update this section.

## Limitations and Next Steps

- This is a provided case-study dataset and may not represent a real company's portfolio.
- The 100 projects and reporting history may not represent larger or more complex portfolios.
- Project records do not all have the same latest reporting date; freshness should be checked before decisions.
- The action thresholds are case-study assumptions and should be agreed with business stakeholders before use in a real PMO.
- The formula behind the source risk exposure score was not independently recreated.
- Missing benefit-realisation values need context; they should not automatically be treated as zero.
- SQL was not used in this version.
- Next steps: validate decision thresholds with stakeholders, test slicers and tooltips, publish the report, add real project links, and optionally reproduce selected checks in SQL as a separate extension.

## What I Learned

- How to connect PMO business questions with measures, data modelling and dashboard design.
- Why data grain, relationship checks and reporting-date freshness matter before interpreting results.
- How to use DAX and report-page tooltips to keep visuals clear while preserving useful detail.
- How to explain rule-based recommendations with clear limitations instead of presenting them as automatic decisions.

## Contact

**Saurabh Sonwane**  
[LinkedIn](https://linkedin.com/in/your-profile) | [Email](mailto:your-email@example.com)

> Replace the LinkedIn and email placeholders with your actual public profile details before publishing.
