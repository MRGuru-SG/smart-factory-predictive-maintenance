# Smart Factory Sensor Intelligence & Predictive Maintenance Analytics

A data analytics portfolio project that explores industrial machine sensor readings to identify failure patterns, detect unusual behaviour, and support preventive maintenance decisions.

> **Dataset note:** This project uses a synthetic dataset for learning and demonstration. Findings describe this dataset and should not be interpreted as results from a real factory.

## Project Overview

Unexpected machine failures can increase downtime, interrupt production, and raise maintenance costs. This project analyses machine sensor and operating data to understand failure patterns and highlight machines that may need closer inspection.

The workflow combines Python-based analysis, SQL querying, and an interactive dashboard to turn raw readings into understandable operational insights.

## Objectives

- Summarise sensor readings and machine failures.
- Compare failure counts, average temperature, and downtime across machine profiles.
- Identify machines with the highest recorded failure counts.
- Explore anomalous sensor behaviour as a potential early-warning signal.
- Present findings through a dashboard and propose practical maintenance actions.

## Dataset

The synthetic dataset contains **12,000 sensor readings** across **20 machines**, with **600 readings per machine**. It includes fields such as:

- `timestamp`
- `machine_id`
- `machine_profile`
- `temperature`
- `vibration`
- `pressure`
- `rpm`
- `current`
- `operating_hours`
- `downtime_minutes`
- `maintenance_status`
- `failure`
- `anomaly`

Machine profiles used in the analysis:

- Healthy
- Moderate Wear
- High Usage
- Older Machine

## Tools & Technologies

- **Python** — data exploration and analysis
- **Pandas** — data manipulation and aggregation
- **SQL / MySQL Workbench** — querying, grouping, filtering, and summarising data
- **HTML, CSS, JavaScript** — interactive dashboard prototype
- **Power BI** — dashboard exploration / visual analytics (if using the Power BI version in your portfolio)

## Verified Dataset Metrics

| Metric | Value |
|---|---:|
| Total sensor readings | 12,000 |
| Total recorded failures | 510 |
| Failure rate | 4.25% |
| Total downtime | 265,696 minutes |
| Machines | 20 |
| Readings per machine | 600 |

**Calculation:** Failure rate = total recorded failures ÷ total sensor readings × 100 = 510 ÷ 12,000 × 100 = **4.25%**.

## Key Findings

### Failures and downtime by machine profile

| Machine profile | Failures | Average temperature | Total downtime (minutes) |
|---|---:|---:|---:|
| Older Machine | 288 | 81.45°C | 122,489 |
| High Usage | 138 | 77.90°C | 76,093 |
| Moderate Wear | 56 | 71.45°C | 35,918 |
| Healthy | 28 | 68.18°C | 31,196 |
| **Total** | **510** | — | **265,696** |

- **Older Machine** has the largest recorded failure count (288) and highest accumulated downtime (122,489 minutes) in this dataset.
- **High Usage** is the second-highest profile by recorded failures (138).
- **Older Machine** also has the highest average temperature (81.45°C) among the four profiles.

### Top 5 machines by recorded failures

| Rank | Machine ID | Readings | Failures | Average temperature (°C) | Downtime (minutes) |
|---:|---|---:|---:|---:|---:|
| 1 | M016 | 600 | 68 | 83.36 | 25,189 |
| 2 | M018 | 600 | 63 | 82.87 | 25,729 |
| 3 | M020 | 600 | 58 | 78.55 | 23,489 |
| 4 | M019 | 600 | 53 | 81.84 | 24,623 |
| 5 | M017 | 600 | 46 | 80.62 | 23,459 |

These machines are useful candidates for deeper investigation in this dataset. A high count alone does not establish the cause of failure.

## Anomaly Detection

An Isolation Forest approach was explored to flag unusual sensor patterns.

- The configured contamination rate was **5%**.
- The model flagged **600 readings** as anomalies out of 12,000.
- The flagged readings are candidates for review, not confirmed machine failures.

Anomaly detection can help prioritise investigation, but its usefulness should be evaluated against maintenance records and validated data before operational use.

## Dashboard

The interactive dashboard prototype includes:

- KPI cards for readings, failures, failure rate, and downtime
- Average temperature by machine profile
- Failures by machine profile
- Top five machines by recorded failures
- Downtime by machine profile
- Machine profile distribution
- Machine profile and machine ID selectors
- Key insights and maintenance recommendations

Suggested file name: `smart_factory_dashboard_reference_style.html`

## SQL Analysis Examples

Example query to calculate the main KPIs:

```sql
SELECT
    COUNT(*) AS total_readings,
    SUM(failure) AS total_failures,
    ROUND(SUM(failure) * 100.0 / COUNT(*), 2) AS failure_rate_pct,
    SUM(downtime_minutes) AS total_downtime_minutes
FROM sensor_data;
```

Example query to compare failures by machine profile:

```sql
SELECT
    machine_profile,
    SUM(failure) AS total_failures,
    ROUND(AVG(temperature), 2) AS avg_temperature,
    SUM(downtime_minutes) AS total_downtime_minutes
FROM sensor_data
GROUP BY machine_profile
ORDER BY total_failures DESC;
```

## Recommendations Based on This Dataset

1. Prioritise review of the Older Machine profile because it has the highest recorded failures and downtime.
2. Investigate the five machines with the highest failure counts to look for common patterns.
3. Monitor temperature and vibration together rather than relying on one sensor alone.
4. Review anomaly flags alongside failure and maintenance records before deciding on maintenance actions.
5. Validate the approach on real, time-ordered factory data before using it for operational decisions.

## Repository Structure

A suggested GitHub repository layout:

```text
smart-factory-predictive-maintenance/
├── README.md
├── smart_factory_dashboard_reference_style.html
├── smart_factory_analysis.sql
├── smart_factory_analysis.ipynb
└── data/
    └── README.md
```

Only include the notebook, SQL file, and data folder once you have those files ready. Do not upload confidential or restricted data.

## How to Use

1. Download or clone this repository.
2. Open the HTML dashboard file in a modern browser.
3. Run the SQL examples in MySQL Workbench after loading the dataset into a table named `sensor_data`.
4. Open the notebook in Jupyter Notebook or Google Colab to review the Python analysis (if included).

## Limitations

- The dataset is synthetic, not real industrial telemetry.
- The failure rate is calculated as recorded failure rows divided by all sensor-reading rows; it is not a machine-level reliability metric.
- Dashboard filters in the HTML prototype use the summary values built into the page. For a production-ready dashboard, connect the visuals to the full dataset and validate all filtered calculations.
- Anomaly flags indicate unusual patterns, not guaranteed future failures.
- The reported relationships are descriptive and do not prove that temperature, age, or usage caused failures.

## Future Improvements

- Connect all visuals to the complete dataset and validate filter behaviour.
- Add time-series trends for temperature, vibration, and failures.
- Evaluate anomaly detection against labelled maintenance outcomes.
- Add a maintenance-priority score with clearly documented rules.
- Build a fully data-connected Power BI report.

## Author

**Data Analytics Portfolio Project**  
Focus areas: Python, Pandas, SQL, data analysis, anomaly detection, and dashboard storytelling.
