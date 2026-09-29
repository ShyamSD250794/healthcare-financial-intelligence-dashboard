# KPI Definitions

## Overview

This document defines the key financial and operational indicators used in the Healthcare Financial Intelligence Dashboard.

The KPIs support four analytical areas:

- Financial performance
- Peer benchmarking
- Facility risk monitoring
- Data quality and exceptions

Financial metrics are evaluated at the facility and reporting-quarter level. Peer comparisons use the hospital's peer group and reporting quarter, subject to data availability.

## 1. Financial Performance KPIs

| KPI | Definition | Interpretation |
|---|---|---|
| Net Patient Revenue | Revenue generated from patient-care services, as represented in the source data. | Indicates the scale of a facility's patient-service revenue. It is not the same as net income or profit. |
| Operating Margin | Operating profitability expressed as a percentage, using the operating-margin calculation in the financial ratios view. | A higher positive margin indicates more operating revenue retained after operating expenses, under the implemented definition. |
| Total Margin | Overall financial margin expressed as a percentage, using the total-margin calculation in the financial ratios view. | Reflects the facility's overall financial result under the implemented definition. |
| Return on Assets (ROA) | Return generated relative to the facility's asset base, using the ROA calculation in the financial ratios view. | Provides an indication of how effectively assets generate financial returns. |
| Current Ratio | Current assets relative to current liabilities, using the current-ratio calculation in the financial ratios view. | A ratio above 1 generally indicates that current assets exceed current liabilities. Interpretation should consider the facility's circumstances and the composition of its current assets. |
| Days Cash on Hand | An estimate of how many days a facility could cover relevant expenses using available cash and investments, based on the implemented calculation. | Higher values generally indicate a larger cash reserve relative to daily expenses. |
| Net Long-Term Debt / Assets | Net long-term debt expressed relative to total assets, using the implemented financial-ratio calculation. | Indicates the scale of long-term debt relative to the facility's asset base. Higher values may indicate greater leverage. |

**Calculation note:** The underlying Oracle SQL views and Tableau calculated fields are the source of truth for the exact numerator, denominator, aggregation, and treatment of missing values for each KPI.

## 2. Peer Benchmarking Metrics

### Peer Median

The peer median is the median value for eligible facilities in the same hospital-type group and reporting quarter.

- The selected hospital is excluded from its own peer comparison.
- Peer medians are calculated for the relevant reporting quarter.
- A peer median is unavailable when a valid comparison group cannot be formed.
- Shriners is a single-facility peer group in this project; its peer median is therefore unavailable.

The median is used instead of the mean to reduce the influence of unusually high or low observations.

### Difference from Peer Median

For metrics where a difference is meaningful:

**Difference = Selected Hospital KPI − Peer Median KPI**

For percentage-based metrics, the difference may be expressed in percentage points (pp). For example, an operating margin of 4.83% compared with a peer median of 1.35% represents a difference of **+3.48 percentage points**.

### Percentage Difference from Peer Median

Where applicable:

**Percentage Difference = (Selected Hospital KPI − Peer Median KPI) ÷ Peer Median KPI × 100**

Percentage differences should be interpreted carefully when the peer median is zero, close to zero, negative, or unavailable.

### Peer Rank

Peer rank represents the selected facility's position among eligible facilities for the chosen metric and comparison group.

The rank is dependent on the metric, reporting quarter, eligible comparison population, and ranking direction used in the dashboard.

## 3. Facility Risk Indicators

The Facility Risk Monitor highlights rule-based indicators that may warrant further review.

Examples include:

- Negative equity
- High leverage
- Other financial or operational conditions captured by the project's risk rules

Risk flags are screening indicators, not a complete assessment of a facility's financial condition. A flagged facility should be reviewed in context rather than treated as automatically distressed.

A facility may have multiple flags. The dashboard summarizes the number and types of flags to help users identify records for further investigation.

## 4. Data Quality Metrics

| Metric | Definition |
|---|---|
| Facility-Quarter Records Checked | Number of facility-quarter records included in the relevant data-quality checks. |
| Financial QA Pass | Records passing the project's financial validation rules. |
| Bed Count Reported | Records with a reported bed-count value, according to the project's data-quality logic. |
| Data Checks to Review | Records or checks identified for further review by the implemented exception rules. |
| Negative Equity Flags | Records identified by the negative-equity rule. |

A blank value represents unavailable or unreported information where applicable; it should not automatically be interpreted as zero.

## 5. Interpretation Guidelines

- Compare facilities using the same reporting quarter and appropriate peer group.
- Distinguish revenue from profitability: net patient revenue is not net income.
- Interpret financial ratios alongside the underlying financial context.
- Treat risk flags and data-quality exceptions as prompts for investigation, not confirmed errors.
- Review missing values before drawing conclusions.
- Use the dashboard's selected hospital and quarter controls to understand the scope of each comparison.

## Related Documentation

- [Data Dictionary](Data_Dictionary.md)
- [Methodology](Methodology.md)
