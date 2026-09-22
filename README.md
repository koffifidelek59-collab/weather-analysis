# 🌦️ Weather and Climate Pattern Analysis

**KOUAME Koffi Fidèle**
*Data Analysis Internship | Energy Systems & Data Analytics*
📧 `koffifidelek59@gmail.com`

> **A reproducible end-to-end weather data analysis project combining data quality assessment, statistical analysis, visualization, and an interactive Power BI dashboard.**

---

## 📊 Project Overview

This project analyses a **single-station daily weather record containing 3,271 observations from February 2008 to June 2017**.

The objective is to move beyond basic data cleaning and investigate whether the dataset is sufficiently reliable to support conclusions about:

* 🌡️ Temperature variability and long-term trends
* 🌧️ Rainfall patterns
* 💧 Humidity behaviour
* 💨 Wind direction and speed
* 📅 Seasonal and monthly variability
* 📈 Relationships between meteorological variables
* 🔎 Data-quality and reliability issues

The project follows a complete data-analysis workflow:

**Data Validation → Data Quality Assessment → Exploratory Analysis → Statistical Testing → Visualization → Power BI Dashboard → Insights**

---

## 🎯 Key Results

Although the dataset contains **0 missing cells and 0 duplicate rows**, deeper analysis identified three important issues that a conventional completeness check would not detect.

### 1. 💨 Repetitive Wind Pattern

The combination **West + 41 km/h** appears on **1,027 days**, representing **31.4% of the dataset**.

The pattern is particularly unusual because it occurs:

* On every recorded day in **2008 and 2009**
* On approximately **80% of observations in 2010**
* At a frequency **32 times higher** than the next most common direction-speed combination

After applying the reliability assessment, the proportion of westerly winds decreases from **43.6% of the complete record to 17.7% of the reliable observations**.

This demonstrates why **data reliability cannot be evaluated using missing-value checks alone**.

---

### 2. 📅 Missing Calendar Days

The dataset contains no missing cells, but **162 calendar days have no observation at all**.

This distinction is important:

> A missing row cannot appear as a missing cell because the row itself does not exist.

Monthly observation coverage is therefore unequal, ranging from approximately **240 to 310 observed days**.

To avoid misleading comparisons, monthly rainfall and other aggregates are evaluated using both:

* **Raw totals**
* **Values normalised by the number of observed days**

---

### 3. 🌍 No Spatial Information

The original analysis brief refers to comparisons across cities and countries.

However, the dataset does not contain:

* City
* Country
* Station ID
* Latitude
* Longitude

Therefore, this project intentionally treats the dataset as a **single-station temporal record**.

No unsupported spatial comparison is introduced.

---

## 📈 Statistical Findings

### 🌡️ Temperature Trend

A statistical trend analysis was performed using the **eight complete years** in the record.

Years with insufficient coverage were excluded.

| Metric          |                Result |
| --------------- | --------------------: |
| Estimated trend | **+1.51 °C / decade** |
| p-value         |             **0.020** |
| R²              |              **0.62** |

The results indicate a positive temperature trend within the analysed station record.

This result should be interpreted specifically as a trend in the available dataset and not as a direct estimate of regional or global climate change.

---

### 🌧️ Rainfall

Rainfall was evaluated using both absolute totals and rainfall normalised by observed-day coverage.

**June is the wettest month under both approaches.**

This agreement is important because the dataset contains unequal temporal coverage.

The analysis also identifies:

**849 rainy days**

The Power BI dashboard should therefore display the value as **849**, rather than using a rounded `1K` display unit.

---

### 💨 Wind

After accounting for the identified reliability issue:

| Wind direction |     Share |
| -------------- | --------: |
| **West**       | **17.7%** |
| Southeast      |  **4.5%** |

The original dashboard statement identifying **SE as the dominant wind direction** was therefore corrected.

---

### 💧 Humidity

The highest humidity values occur in **February**.

Seasonal interpretation was based on the dataset itself: January is the warmest month, supporting the use of the **Southern Hemisphere seasonal convention**.

---

## 🧪 Data Quality Methodology

The project does not modify the data before measuring the problem.

The workflow is:

```text
Raw Dataset
     ↓
Data Inspection
     ↓
Date Validation
     ↓
Missing & Duplicate Checks
     ↓
Calendar Coverage Analysis
     ↓
Range & Consistency Checks
     ↓
Reliability / Anomaly Detection
     ↓
Exploratory Data Analysis
     ↓
Monthly & Seasonal Analysis
     ↓
Statistical Trend Analysis
     ↓
Power BI Dashboard
     ↓
Insights & Recommendations
```

### Date Validation

The date format was tested rather than assumed.

An incorrect `d/m/Y` interpretation leaves approximately **60% of the observations unparsed**, confirming that the date format must be validated before analysis.

### Seasonal Classification

The warmest month is **January**, so the seasonal classification used in the analysis is:

| Season    | Months               |
| --------- | -------------------- |
| ☀️ Summer | December – February  |
| 🍂 Autumn | March – May          |
| ❄️ Winter | June – August        |
| 🌱 Spring | September – November |

---

## 📊 Power BI Dashboard

The project includes an interactive **Power BI dashboard** with:

* KPI cards
* Temperature analysis
* Rainfall analysis
* Humidity indicators
* Wind analysis
* Seasonal comparisons
* Interactive filtering
* Custom visual theme
* Reliability-aware analysis

### Dashboard Quality Review

Four dashboard statements were reviewed after completing the analytical workflow:

| Original item                    | Corrected result |
| -------------------------------- | ---------------- |
| Rainy Days: `1K`                 | **849**          |
| Highest rainfall month: February | **June**         |
| Humidity peaks: winter           | **February**     |
| Dominant wind: SE                | **West**         |

---

## 📊 Visualizations

The project produces dedicated visualizations covering:

* Calendar coverage
* Temperature cycle
* Rainfall patterns
* Wind distribution
* Long-term temperature trend
* Variable relationships
* Power BI dashboard

---

## 🛠️ Technologies

| Category              | Tools                   |
| --------------------- | ----------------------- |
| Programming           | **Python**              |
| Data manipulation     | **Pandas, NumPy**       |
| Visualization         | **Matplotlib, Seaborn** |
| Statistics            | **SciPy**               |
| Notebook              | **Jupyter Notebook**    |
| Business Intelligence | **Power BI**            |
| Reporting             | **LaTeX**               |
| Version Control       | **Git / GitHub**        |

---

## 📁 Project Structure

```text
Weather_Analysis/
│
├── 📓 Weather_Analysis.ipynb
├── 📄 Weather_Climate_Report.pdf
├── 📄 INSIGHTS.md
├── 📄 DASHBOARD_FIXES.md
├── 🐍 analysis.py
├── 📄 report.tex
├── 📊 Weather_Dashboard.pbix
├── 🎨 WeatherDashboard.json
│
├── data/
│   ├── Weather_Data_original.csv
│   ├── weather_clean.csv
│   └── weather_clean_extended.csv
│
├── figures/
│   ├── 01_coverage.png
│   ├── 02_temperature_cycle.png
│   ├── 03_rainfall.png
│   ├── 04_wind_rose.png
│   ├── 05_trend.png
│   ├── 06_relationships.png
│   └── 07_powerbi_dashboard.png
│
└── results/
    ├── annual_means.csv
    ├── correlation.csv
    ├── findings.json
    ├── monthly_profile.csv
    └── seasonal_profile.csv
```

---

## 🚀 How to Run

### 1. Clone the repository

```bash
git clone <YOUR_REPOSITORY_URL>
cd Weather_Analysis
```

### 2. Install dependencies

```bash
pip install pandas numpy matplotlib scipy
```

### 3. Run the analysis

```bash
python analysis.py
```

### 4. Open the notebook

Launch:

```text
Weather_Analysis.ipynb
```

The notebook can also be executed using **Google Colab**.

---

## 📦 Deliverables

| Deliverable             | Status |
| ----------------------- | :----: |
| Cleaned dataset         |    ✅   |
| Data quality assessment |    ✅   |
| Exploratory analysis    |    ✅   |
| Statistical analysis    |    ✅   |
| Visualization suite     |    ✅   |
| Power BI dashboard      |    ✅   |
| Dashboard validation    |    ✅   |
| Analytical insights     |    ✅   |
| PDF report              |    ✅   |
| Reproducible notebook   |    ✅   |

---

## 💡 Main Analytical Lessons

This project highlights several important principles of professional data analysis:

> **A dataset can contain zero missing cells and still contain serious data-quality problems.**

> **Missing observations and missing values are not the same thing.**

> **Aggregated statistics should account for unequal temporal coverage.**

> **Statistical trends should be tested rather than inferred solely from visualizations.**

> **A dashboard should communicate validated results, not assumptions.**

---

## 🔎 Limitations

The analysis should be interpreted within the limitations of the available dataset:

* Single-station record
* No geographical metadata
* 162 missing calendar days
* Unequal monthly coverage
* Repetitive wind observations
* Incomplete coverage for some years

These limitations do not invalidate the analysis; instead, they define the scope within which the results can reasonably be interpreted.

---

## 🔮 Future Improvements

Future versions could integrate:

* 🌍 Multi-station and multi-country datasets
* 🛰️ Satellite and reanalysis data
* 🌞 Solar radiation and GHI
* 💨 More complete wind observations
* 🌧️ Extreme rainfall analysis
* 🤖 Machine learning for weather forecasting
* 📊 Automated Power BI data refresh
* ⚡ Integration with energy-system analysis
* 💧 Applications to renewable energy and green hydrogen production

---

## 👤 Author

### **KOUAME Koffi Fidèle**

**Energy Systems Analyst | AI for Power Systems & Green Hydrogen | Machine Learning**

Interested in the intersection of:

**Data Analytics · Energy Systems · Renewable Energy · Green Hydrogen · Machine Learning**

📧 `koffifidelek59@gmail.com`

---

⭐ **If you find this project useful, feel free to explore the repository and its analytical workflow.**
