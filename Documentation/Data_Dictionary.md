# Data Dictionary

## Overview

This document describes the primary fields, analytical views, and business concepts used in the Healthcare Financial Intelligence Dashboard.

The project uses Oracle SQL views as the analytical layer consumed by Tableau. Field names shown below reflect the major concepts used throughout the dashboard rather than every column available in the underlying source data.

## 1. Facility & Organizational Fields

| Field | Description |
|---|---|
| Fac Name | Name of the healthcare facility. |
| Type Hosp | Hospital or facility type used for classification and peer grouping. |
| Facility ID | Identifier used to distinguish facilities where available. |
| County | County associated with the facility. |
| Latitude | Geographic latitude used for facility mapping. |
| Longitude | Geographic longitude used for facility mapping. |

## 2. Reporting Period Fields

| Field | Description |
|---|---|
| Year Qtr | Reporting-period identifier used throughout the analytical views. |
| Quarter | Human-readable reporting quarter used in Tableau visualizations. |
| Selected Quarter | Dashboard parameter controlling the reporting quarter displayed in quarter-specific analyses. |

Reporting periods are evaluated at the facility-quarter level where applicable.

## 3. Financial Fields

| Field | Description |
|---|---|
| Net Tot | Net patient revenue represented in the analytical dataset. |
| Operating Margin Pct | Operating margin expressed as a percentage. |
| Total Margin Pct | Total margin expressed as a percentage. |
| Current Ratio | Current assets relative to current liabilities. |
| Days Cash on Hand | Estimated number of days of relevant expenses that available cash and investments can cover. |
| Net LT Debt / Assets | Net long-term debt relative to total assets. |
| ROA | Return on assets. |

The exact calculation logic for financial ratios is implemented in the Oracle analytical views.

## 4. Peer Benchmarking Fields

| Field | Description |
|---|---|
| Peer Median | Median KPI value for eligible facilities in the same peer group and reporting quarter. |
| Peer Median Net Tot | Median net patient revenue for the relevant peer group and quarter. |
| Peer Group | Facilities classified into the same hospital-type comparison group. |
| Revenue vs Peer Median | Difference between the selected hospital's net patient revenue and the peer median. |
| Percentage Difference | Percentage difference between the selected hospital KPI and the peer median. |
| Peer Rank | Position of the selected facility relative to eligible facilities for the selected metric. |

The selected hospital is excluded from its own peer comparison.

## 5. Risk Fields

| Field | Description |
|---|---|
| Risk Flag | Indicator that a facility meets one of the implemented risk rules. |
| Risk Type | Category of the identified risk indicator. |
| Risk Count | Number of risk indicators associated with a facility. |
| Negative Equity Flag | Indicates that the facility meets the project's negative-equity rule. |
| High Leverage Flag | Indicates that the facility meets the project's leverage-related risk rule. |
| Review Watchlist | Facilities identified for further review based on the implemented risk logic. |

Risk fields represent rule-based screening indicators and not confirmed financial problems.

## 6. Data Quality Fields

| Field | Description |
|---|---|
| Checked | Indicates that a facility-quarter record was included in the relevant validation check. |
| Fin Pass | Indicates whether the record passed the applicable financial validation rule. |
| Bed Pass | Indicates whether the record satisfied the applicable bed-count validation rule. |
| Data Check | Indicates that a record requires review under the project's data-quality logic. |
| Negative Equity | Indicates that negative equity was identified during the relevant data-quality check. |
| Exception | Identifies records requiring additional data-quality investigation. |

## 7. Dashboard Parameter Fields

| Parameter | Purpose |
|---|---|
| Selected Hospital | Controls the facility selected for peer benchmarking analysis. |
| P1 - Selected Quarter | Controls the reporting quarter used by quarter-specific dashboard analyses. |

The default selected hospital for the peer benchmarking workflow is **Howard Memorial**.

## 8. Analytical Views

The primary Oracle views supporting the Tableau workbook include:

| View | Purpose |
|---|---|
| `VW_FACILITY_LOCATION` | Facility geographic and organizational information. |
| `VW_FACILITY_RATIOS` | Facility-level financial ratios and performance metrics. |
| `VW_FACILITY_RISK` | Facility-level risk indicators. |
| `VW_KPI_TRENDS` | Historical KPI trends across reporting periods. |
| `VW_PEER_BENCHMARK` | Peer benchmarking calculations and comparison metrics. |
| `VW_PEER_METRICS_LONG` | Long-format peer KPI data used for benchmarking analysis. |
| `VW_PEER_INSIGHTS` | Peer comparison insights used by the dashboard. |
| `VW_RISK_KPI` | Risk KPI summaries used by the Facility Risk Monitor. |
| `VW_RISK_WATCHLIST` | Facilities identified for risk review. |
| `VW_DQ_EXCEPTIONS` | Data-quality exceptions requiring review. |
| `VW_DQ_KPI` | Data-quality KPI and validation summaries. |
| `VW_REVENUE_OUTLIERS` | Revenue observations identified for outlier review. |

## 9. Value Conventions

The dashboard follows these general conventions:

- **Blank** = information is unavailable or not reported.
- **Zero** = an actual zero value where supported by the source data.
- **Percentage (%)** = ratio expressed as a percentage.
- **Percentage points (pp)** = arithmetic difference between two percentage values.
- **Median** = middle value of the eligible comparison population.
- **Risk flag** = rule-based indicator requiring review, not a confirmed error.
- **Outlier flag** = observation identified for investigation, not an automatically invalid record.

## 10. Data Interpretation Notes

### Net Patient Revenue

Net patient revenue represents patient-service revenue in the analytical dataset. It should not be interpreted as net income or profit.

### Peer Medians

Peer medians are calculated using comparable facilities in the same hospital-type group and reporting quarter, excluding the selected hospital.

### Singleton Peer Groups

When a hospital type contains only one facility, an independent peer comparison cannot be calculated.

Shriners is treated as a singleton peer group in this project, so its peer median is unavailable.

### Occupancy

Occupancy values above 100% are retained as informational observations because they may occur during periods of unusually high utilization or surges.

## Related Documentation

- [KPI Definitions](KPI_Definitions.md)
- [Methodology](Methodology.md)
