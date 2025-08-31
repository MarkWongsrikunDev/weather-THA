# weather-THA
Goal: Ingest hourly/daily weather for selected cities (e.g., Bangkok, Chiang Mai, Phuket), enforce data quality, model into analytics tables, and publish insights/dashboards.

Stack: Python · Airflow · Great Expectations (v0.18.x) · SQL (SQLite/DuckDB for portability, optional MS SQL/BigQuery) · dbt (optional) · Power BI (or a notebook dashboard) · Docker (optional)

flowchart LR
A[APIs: Open-Meteo (no-key) / OpenWeatherMap (key)] --> B[Extract: Python]
B --> C[Bronze: raw JSON/Parquet]
C --> D[GE Validations]
D --> E[Silver: cleaned tables]
E --> F[dbt/SQL: dims & facts (Gold)]
F --> G[Dashboards (Power BI / Notebook)]
subgraph Orchestration
  H[Airflow DAG] --> B
  H --> D
  H --> E
  H --> F
end
