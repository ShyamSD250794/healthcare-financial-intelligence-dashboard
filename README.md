# 🏥 Healthcare Financial Intelligence Dashboard

A Tableau-based healthcare analytics dashboard designed to analyze hospital financial performance, peer benchmarking, facility risk, and data quality across California hospitals.

## 📊 Dashboard Preview

### Financial Overview
![Financial Overview](Screenshots/financial_overview.png)


### Peer Benchmarking
![Peer Benchmarking](Screenshots/peer_benchmarking.png)


### Facility Risk Monitor
![Facility Risk Monitor](Screenshots/facility_risk_monitor.png)


### Data Quality & Exceptions
![Data Quality & Exceptions](Screenshots/data_quality_exceptions.png)



## 🎬 Interactive Demo

### Peer Benchmarking

Demonstrates dynamic hospital and quarter selection and how the peer benchmarking metrics respond to user selections.

![Peer Benchmarking Interaction](Demo/peer_benchmarking_interaction.gif)

### Facility Risk Monitor

Demonstrates quarter-driven updates across the risk KPIs, risk profile, flagged risks, facility map, and review watchlist.

![Facility Risk Monitor Interaction](Demo/facility_risk_monitor_interaction.gif)


## 📖 Project Overview

This project demonstrates an end-to-end healthcare financial analytics workflow using Oracle SQL and Tableau.

The dashboard focuses on four key areas:

- Hospital financial performance
- Peer benchmarking
- Facility risk monitoring
- Data quality and exceptions

## 🖥️ Dashboard Pages

### 1. Financial Overview

Provides a high-level view of hospital financial performance and financial trends.

### 2. Peer Benchmarking

Compares a selected hospital against its peer group using financial and operating metrics.

### 3. Facility Risk Monitor

Identifies facilities with rule-based financial risk indicators requiring review.

### 4. Data Quality & Exceptions

Highlights data-quality checks, exceptions, and records requiring manual review.

## 🛠️ Tools & Technologies

- Tableau
- Oracle SQL
- SQL Views
- Data Quality & Validation
- Financial Analytics
- Peer Benchmarking
- Risk Analytics

## 📂 Source

### California Hospital Quarterly Financial & Utilization Report

This project uses the publicly available **Hospital Quarterly Financial & Utilization Report – Complete Data Set** published through HealthData.gov.

**Source:**  
[California Hospital Quarterly Financial & Utilization Report](https://healthdata.gov/State/Hospital-Quarterly-Financial-Utilization-Report-Co/8j3z-qxvr/about_data)

The source data was used as the foundation for the hospital financial, operational, peer benchmarking, risk monitoring, and data-quality analysis presented in this project.

Detailed information on data preparation, SQL transformations, KPI definitions, peer methodology, validation, and analytical logic is available in the `Documentation` folder.

## 📁 Repository Contents

```text
Healthcare-Financial-Intelligence-Dashboard/
│
├── README.md
│
├── Documentation/
│   ├── Data_Dictionary.md
│   ├── KPI_Definitions.md
│   └── Methodology.md
│
├── Tableau/
│   └── Healthcare_Financial_Intelligence_Dashboard.twbx
│
├── Screenshots/
│   ├── Financial_Overview.png
│   ├── Peer_Benchmarking.png
│   ├── Facility_Risk_Monitor.png
│   └── Data_Quality_Exceptions.png
│
├── Demo/
│   ├── Peer_Benchmarking_Interaction.gif
│   └── Facility_Risk_Monitor_Interaction.gif
│
└── SQL/
    └── Project3_Oracle_SQL_Final.sql

```

## 👨‍💻 Author

**Shyam Das**

*Business Intelligence / Data Analytics Portfolio Project*

### Project Focus

- Healthcare Financial Analytics
- Tableau Dashboard Development
- Oracle SQL
- Peer Benchmarking
- Risk Monitoring
- Data Quality & Validation





