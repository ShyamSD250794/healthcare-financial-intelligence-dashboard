# Methodology

## Overview

The Healthcare Financial Intelligence Dashboard follows a multi-stage analytics workflow combining source data preparation, Python-based exploratory checks, Oracle SQL transformation and validation, and Tableau visualization.

The overall workflow is:

**Source Excel Data → Python Exploration & QA → Oracle SQL Transformation & Validation → Tableau Dashboard**

Each layer served a different purpose in the development process.

## 1. Source Data

The project uses the publicly available **California Hospital Quarterly Financial & Utilization Report – Complete Data Set**.

The source data contains hospital-level financial, operational, utilization, and organizational information across reporting quarters.

The source dataset was initially worked with in Excel to understand the available fields, structure, reporting periods, and potential data-quality issues.

Excel was used as an initial data inspection and working layer rather than as the final analytical or visualization layer.

## 2. Python Exploration & Data Quality Checks

Python was used during the development process for exploratory analysis and initial data-quality investigation.

These checks were used to examine areas such as:

- Missing values
- Data distributions
- Potential outliers
- Unexpected values
- Field completeness
- General data consistency
- Relationships between important financial and operational fields

The Python analysis helped identify areas requiring additional validation and informed the subsequent SQL transformation and validation work.

Python was primarily an exploratory and supporting QA layer. The final analytical views consumed by Tableau were implemented and validated in Oracle SQL.

## 3. Oracle SQL Transformation Layer

The cleaned and investigated data was loaded into an Oracle database environment.

Oracle SQL was then used to create the analytical transformation layer consumed by Tableau.

Key analytical views include:

- `VW_FACILITY_LOCATION`
- `VW_FACILITY_RATIOS`
- `VW_FACILITY_RISK`
- `VW_KPI_TRENDS`
- `VW_PEER_BENCHMARK`
- `VW_PEER_METRICS_LONG`
- `VW_PEER_INSIGHTS`
- `VW_RISK_KPI`
- `VW_RISK_WATCHLIST`
- `VW_DQ_EXCEPTIONS`
- `VW_DQ_KPI`

The SQL layer separates data preparation, business logic, KPI calculations, peer methodology, risk rules, and validation from the Tableau presentation layer.

## 4. Financial Analytics

Financial performance is evaluated at the facility and reporting-quarter level.

The dashboard uses financial and operating indicators including:

- Net Patient Revenue
- Operating Margin
- Total Margin
- Current Ratio
- Days Cash on Hand
- Net Long-Term Debt / Assets
- Return on Assets

The exact KPI calculations are implemented in the Oracle analytical views and validated against the underlying data.

## 5. Peer Benchmarking

Peer benchmarking compares a selected hospital with comparable facilities.

The peer methodology uses:

- The same reporting quarter
- The same hospital-type classification
- Exclusion of the selected hospital from its own peer group

Peer medians are used as the primary benchmark.

The median was selected to reduce the influence of unusually high or low observations within a peer group.

### Peer Comparison

For a selected KPI:

**Difference = Selected Hospital KPI − Peer Median KPI**

Where appropriate:

**Percentage Difference = (Selected Hospital KPI − Peer Median KPI) ÷ Peer Median KPI × 100**

Peer comparisons are only presented where a valid comparison population is available.

### Singleton Peer Groups

Some hospital types may contain only one facility.

Shriners is a singleton peer group in this project. Because there is no independent facility available for comparison, a peer median is not calculated.

The dashboard displays this as unavailable rather than treating the missing benchmark as zero.

## 6. Facility Risk Monitoring

The Facility Risk Monitor uses rule-based indicators to identify facilities requiring further review.

Examples include:

- Negative equity
- High leverage
- Other financial or operational conditions defined by the project's risk logic

Risk indicators are designed as screening mechanisms.

A risk flag does **not** represent a confirmed financial problem or a comprehensive assessment of a facility's financial condition.

The dashboard allows users to examine the number and types of indicators associated with facilities during a selected reporting quarter.

## 7. Data Quality & Validation

Data-quality validation was performed across the development workflow.

Python was used for exploratory data-quality investigation, while Oracle SQL was used for structured validation of the analytical datasets and dashboard metrics.

Validation includes checks for:

- Facility-quarter completeness
- Financial calculation validity
- Bed-count availability
- Data exceptions
- Negative equity conditions
- Unexpected or potentially anomalous values

The Data Quality & Exceptions dashboard exposes the results of these checks so users can distinguish between analytical results and records requiring further review.

## 8. Missing Values

Missing values are preserved where the source does not provide usable information.

A blank value represents unavailable or unreported information and is not automatically converted to zero.

This distinction is particularly important for:

- Peer benchmarks
- Bed counts
- Occupancy
- Financial ratios

For example, two Kaiser regional entities report no beds in the source data. Their occupancy values are therefore left blank rather than interpreted as zero occupancy.

## 9. Outlier and Exception Handling

Outliers and exceptions are surfaced for investigation rather than automatically removed from the analytical dataset.

This approach preserves the underlying observations while allowing users to identify records that may require additional validation.

Examples include:

- Unusually high or low financial values
- Negative equity
- Missing operational information
- Occupancy values above 100%

Occupancy above 100% can occur during periods of high utilization or surges and is therefore treated as informational rather than automatically classified as an error.

## 10. Tableau Dashboard Design

The Tableau workbook organizes the analysis into four dashboards.

### Financial Overview

Provides a high-level view of hospital financial performance and historical trends.

### Peer Benchmarking

Allows users to select a hospital and reporting quarter and compare financial performance with the relevant peer group.

### Facility Risk Monitor

Provides a quarter-based view of facility risk indicators, including risk profiles, flagged risks, geographic distribution, and a review watchlist.

### Data Quality & Exceptions

Provides transparency into data validation, missing information, exceptions, and records requiring review.

## 11. Dashboard Parameters

The dashboard uses parameter-driven selections for:

- Selected Hospital
- Selected Quarter

The selected hospital defaults to **Howard Memorial** for the peer benchmarking workflow.

The selected quarter controls are used to update quarter-specific analytical views while preserving historical trend information where appropriate.

## 12. Validation Approach

Analytical results were validated by comparing Tableau outputs against Oracle SQL results from the underlying analytical views.

Validation was performed for:

- Facility-level financial values
- Peer median calculations
- KPI calculations
- Risk indicators
- Data-quality counts
- Reporting-quarter results

This approach helps ensure that dashboard values are consistent with the underlying analytical layer.

## 13. Reproducibility

The Oracle SQL environment was containerized using Docker to provide a consistent local database environment for development, testing, and validation.

The containerized environment was used to execute the SQL transformation pipeline and validate the analytical views consumed by Tableau.

Connection credentials and environment-specific secrets are not included in the repository.

Python and Excel were used during development and analysis but are not included as repository dependencies because the final dashboard is driven by the Oracle analytical layer and Tableau workbook.

## 14. Analytical Limitations

The dashboard is intended for analytical exploration and portfolio demonstration.

Important limitations include:

- Peer comparisons depend on the availability and classification of comparable facilities.
- Risk indicators are rule-based and are not a comprehensive financial risk assessment.
- Missing source data can limit individual KPI comparisons.
- Historical reporting values may reflect source-system definitions and reporting practices.
- Outlier and exception flags indicate records for review rather than confirmed data errors.

## Related Documentation

- [KPI Definitions](KPI_Definitions.md)
- [Data Dictionary](Data_Dictionary.md)
