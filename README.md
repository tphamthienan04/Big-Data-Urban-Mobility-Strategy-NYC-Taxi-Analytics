# 🚕 Big Data & Urban Mobility Strategy: NYC Taxi Analytics

![Apache Spark](https://img.shields.io/badge/Apache_Spark-FFFFFF?style=for-the-badge&logo=apachespark&logoColor=#E35A16)
![Databricks](https://img.shields.io/badge/Databricks-FF3621?style=for-the-badge&logo=Databricks&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)

## 📌 Executive Summary
This project leverages **Apache Spark (PySpark)** on the **Databricks** platform to analyze over 81 million New York City Yellow Taxi trip records. Moving beyond basic descriptive statistics, this diagnostic analysis uncovers hidden urban mobility paradigms, such as spatial pricing inequities (The "Commuter Penalty") and operational fleet bottlenecks (The "Mid-Day Valley" Paradox). 

The findings are translated into macro-level, data-driven operational strategies designed to optimize fleet utilization and improve urban transit equity.

## 🛠️ Tech Stack & Methodology
*   **Big Data Processing:** Apache Spark (PySpark), Spark SQL.
*   **Environment:** Databricks Cluster.
*   **Data Visualization:** Python (Pandas, Seaborn, Matplotlib).
*   **Statistical Approach:** Replaced traditional Mean/Standard Deviation with **Median** and **Interquartile Range (IQR)** to account for right-skewed pricing distributions caused by traffic congestion and toll outliers.

## ⚙️ Data Engineering & Cleansing Pipeline
Handling millions of spatial records requires strict data governance to eliminate GPS anomalies and logging errors. The PySpark pipeline enforces the following rules:
*   Filtered out logical errors: Negative/zero fares, zero trip distances, and zero passenger counts.
*   Enforced minimum thresholds: Base fare `> $2.50`, distance `> 0.1 miles`.
*   Bounded physics: Constrained vehicle speeds between `2 mph` and `80 mph` to filter out heavy traffic anomalies and speeding errors.

*Result:* Successfully refined the raw dataset down to **81,749,715 clean, highly reliable records**.

## 🧠 Key Analytical Insights

### 1. Pricing Reliability & The "Commuter Penalty"
By analyzing the Median Fare per Mile against Fare Volatility (IQR), the data exposes severe spatial disparities. 
*   **High-Efficiency Stability:** JFK Airport routes maintain an incredibly stable IQR of $0.33, proving the operational success of flat-rate policies.
*   **The Commuter Penalty:** Outer-borough commuters (e.g., Williamsburg, Long Island City) suffer extreme peak surcharges of up to 27%, structurally driven by their unavoidable reliance on arterial toll bridges.

*<img width="992" height="630" alt="image" src="https://github.com/user-attachments/assets/677a64c9-4428-4a2d-be98-f88b968f586a" />*
`![Pricing Reliability]`

### 2. System Imbalances: "Sinks", "Sources", and "Commuter Tides"
By calculating the Net Accumulation of vehicles (Drop-offs minus Pickups), the system's inability to self-balance becomes visible.
*   **Morning Peak (7 AM - 10 AM):** Centripetal flow turns Midtown Center into a massive oversupply "Sink" (excess of 530,000+ drop-offs).
*   **Evening Peak (4 PM - 7 PM):** Centrifugal flow reverses the pattern, turning Midtown into an undersupply "Source" (deficit of 281,000+ vehicles).

*<img width="1990" height="790" alt="image" src="https://github.com/user-attachments/assets/5586a0c1-25c1-4051-b075-e46ce95a943f" />*
`![Commuter Tides])`

### 3. The "Mid-Day Valley" Paradox
Between 10:00 AM and 4:00 PM, driver utilization plummets. The morning tide leaves a surplus of drivers in Manhattan with insufficient mid-day demand, resulting in severe deadheading (driving empty) and lost revenue.

*<img width="1389" height="586" alt="image" src="https://github.com/user-attachments/assets/f6ddfa7c-0868-4ac3-9885-1beb9973ba4c" />*
`![Mid-Day Valley]`

## 💡 Strategic Recommendations
Based on the diagnostic findings, I propose the following operational transformations:
1.  **Cross-Service Multi-homing:** Integrate taxi fleets with intra-city B2B delivery services during the 11 AM - 2 PM window to absorb the localized mid-day supply surplus.
2.  **Strategic Downtime & EV Hubs:** Deploy high-capacity EV Fast-Charging Hubs in midtown areas to convert mid-day idle time into mandatory charging and rest periods, preventing gridlock from empty cruising.
3.  **Dynamic Repositioning Incentives:** Implement predictive algorithms to offer financial bonuses to drivers who relocate to chronic undersupply zones (e.g., JFK Airport) prior to peak demand surges.

## 📂 Repository Structure
*   `/IPython Notebooks`: Contains the Databricks exported `.ipynb` and `.py` source code utilizing PySpark and Spark SQL.

## 🚀 How to Run
1.  Import the `.ipynb` notebook from the `/notebooks` folder into your Databricks workspace.
2.  Attach the notebook to an active Spark Cluster.
3.  Ensure internet access is enabled on the cluster to dynamically download the `yellow_tripdata_2019` Parquet files via `wget`.
4.  Run all cells to execute the ETL pipeline and generate the visualizations.
