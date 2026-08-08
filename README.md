# 🖥️ IT Infrastructure Health & Anomaly Monitoring Dashboard

## Dashboard Features
Executive KPI Header: Displays total crashes, crash rates, average CPU load, and core operating temperatures.

AI-Powered Line Chart: Tracks CPU load over time with built-in Power BI Anomaly Detection.

Scatter Plot Failure Clustering: Maps CPU load against temperature to visually isolate system crashes.

Interactive Server Filtering: Multi-select dropdown slicer enabling granular drill-down per server node.

## Repository Structure
IT_Infrastructure_Health.pbix — Interactive Power BI Dashboard file.

data/Big_data_dataset.csv — System telemetry dataset.

images/dashboard_screenshot.png — High-resolution preview of the dashboard.

## Executive Summary
This Power BI project provides proactive infrastructure telemetry monitoring for enterprise server farms. By processing 10,000 system logs across 50 simulated cloud servers, the dashboard identifies resource bottlenecks, isolates critical system failure drivers, and leverages native AI Anomaly Detection to flag hardware risks before crashes occur.

---

## 💡 Key Business Insights

* **Failure Causation:** System crashes (`status = 1`) occur exclusively when **CPU Utilization exceeds 89%** and **Server Temperature crosses 84°C**.
* **Resource Optimization:** Power Consumption and Thread Counts remain stable regardless of server failure, indicating that hardware failures are driven by thermal and CPU throttling rather than power supply constraints.
* **Proactive Monitoring:** AI Anomaly Detection flags abnormal CPU utilization spikes across the continuous time-series data, enabling IT operations teams to intervene prior to complete server outages.

---

## 🛠️ Technical Implementation

### Data Pipeline & Modeling
* **Data Ingestion:** Processed 10,000 raw telemetry records (`Big_data_dataset.csv`).
* **Power Query ETL:** Formatted system timestamps, calculated server indices across 50 nodes, and validated data types.
* **Data Architecture:** Engineered a relational model separating telemetry facts from server dimensions.

### Explicit DAX Measures
```dax
// Total Logs Monitored
Total Logs = COUNT('Big_data_dataset'[Index])

// Total Hardware Crashes
System Crashes = CALCULATE([Total Logs], 'Big_data_dataset'[status] = 1)

// Percentage Crash Rate
Crash Rate % = DIVIDE([System Crashes], [Total Logs], 0)

// Average CPU Utilization
Avg CPU = AVERAGE('Big_data_dataset'[cpu_utilization])

// Average Temperature
Avg Temp = AVERAGE('Big_data_dataset'[temperature])
