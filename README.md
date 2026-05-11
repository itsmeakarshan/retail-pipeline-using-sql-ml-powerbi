# Designing an End-to-End SQL and Machine Learning Pipeline for Retail Decision Support

**Student:** Akarshan Rasyal  
**Student ID:** W24040881  
**Programme:** MSc Data Science  
**Supervisor:** Alpana Kumari  
**University:** Northumbria University, Newcastle upon Tyne, UK  

---

## About

This repository contains the complete source code and notebooks for my MSc dissertation project. The project designs, implements, and evaluates an end-to-end data analytics pipeline that integrates Microsoft SQL Server for data preprocessing, Python-based unsupervised machine learning (Isolation Forest and Local Outlier Factor) for anomaly detection, and Microsoft Power BI for interactive visualisation.

## Repository Structure

```
├── src/
│   ├── walmart_pipeline.ipynb              # Primary pipeline (Walmart dataset)
│   └── online_retail_validation.ipynb      # Validation pipeline (Online Retail II dataset)
│
├── data/
│   ├── README.md                           # Instructions to download datasets
│       
├── outputs/
│   ├── walmart_anomaly_results.csv         # Full Walmart results with anomaly scores
│   ├── walmart_anomalies_only.csv          # Flagged anomalies only
│   ├── online_retail_customer_anomalies.csv # Customer-level validation results
│   └── online_retail_anomalies_only.csv    # Flagged customer anomalies only
│
├── dashboard/
│   └── walmart_anomaly_dashboard.pbix      # Power BI dashboard file
│
├── paper/
│   └── dissertation.docx                   # Final dissertation document
│
├── README.md                               # This file
└── requirements.txt                        # Python dependencies
```

## Datasets

The datasets are not included in this repository due to size. Download them from Kaggle:

1. **Walmart Store Sales Forecasting:** https://www.kaggle.com/datasets/gustavoserafim/walmart-recruiting-store-sales-forecasting-gsr
2. **Online Retail II UCI:** https://www.kaggle.com/datasets/mashlyn/online-retail-ii-uci

After downloading, place the files in the `data/walmart/` and `data/online_retail/` folders respectively.

## Prerequisites

- **Docker Desktop** — to run SQL Server
- **Python 3.13** — with Jupyter Notebook
- **Power BI Desktop** — for dashboards (Windows/macOS)

## Setup

### 1. Start SQL Server in Docker

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=<your_password>" -p 1433:1433 --name sql_walmart -d mcr.microsoft.com/mssql/server:2022-latest
```

### 2. Install Python Dependencies

```bash
pip install -r requirements.txt
```

### 3. Run the Notebooks

Open Jupyter Notebook and run the notebooks in order:

1. `notebooks/walmart_pipeline.ipynb` — Primary pipeline
2. `notebooks/online_retail_validation.ipynb` — Validation pipeline

Each notebook is fully documented with step-by-step markdown explanations.

### 4. Open the Dashboard

Open `dashboard/walmart_anomaly_dashboard.pbix` in Power BI Desktop.

## Tools and Technologies

| Tool | Role |
|------|------|
| SQL Server 2022 | Data storage, joins, NULL handling, feature engineering |
| Docker | Containerised SQL Server for reproducibility |
| Python 3.13 | Pipeline orchestration, ML training |
| pyodbc | SQL Server connection from Python |
| SQLAlchemy | Bulk data import, pandas integration |
| Scikit-learn | Isolation Forest, LOF, StandardScaler |
| Pandas / NumPy | Data manipulation |
| Matplotlib | Charts and visualisations |
| Power BI | Interactive dashboards |

## Key Results

- **Isolation Forest** flagged 4,208 anomalies (1.0%) — mostly extreme sales spikes during holidays
- **LOF** flagged 4,216 anomalies (1.0%) — mostly negative sales and density deviations
- **Only 228 records (2.8%)** were flagged by both models, confirming they detect different anomaly types
- **LOF recall on negative sales: 38%** vs IF recall: 1%
- Pipeline successfully validated on Online Retail II dataset (1,067,371 records, 5,939 customers)
