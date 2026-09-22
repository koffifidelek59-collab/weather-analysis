# Weather and Climate Pattern Analysis

**KOUAME Koffi Fidèle** · Data Analysis Internship · koffifidelek59@gmail.com

3,271 daily observations, February 2008 to June 2017

---

## Deliverables

| Required | Delivered | File |
| :--- | :--- | :--- |
| Cleaned data | 3,271 rows, no row deleted | `data/weather_clean.csv` |
| Exploratory analysis | Executed notebook, 10 cells, 6 figures | `Weather_Analysis.ipynb` |
| Visualisations | Six analysis figures | `figures/` |
| Interactive dashboard | Power BI page, cross-filtered, with theme | `Weather_Dashboard.pbix`, `WeatherDashboard.json` |
| Insights | Six insights with recommendations | `INSIGHTS.md`, `Weather_Climate_Report.pdf` |

## Three findings a completeness audit cannot reach

The file has **zero missing cells, zero duplicate rows**, and passes every internal
consistency rule. A routine audit would declare it clean.

**1. Nearly a third of the wind record is a placeholder.** The pair *west, 41 km/h*
occurs on **1,027 days**, 31.4% of the file and 32 times the next most frequent
direction-and-speed combination. It covers **every single day of 2008 and 2009** and
80% of 2010.

West is a legal direction, 41 km/h is inside the observed range of 17 to 96, and the
cells are populated. No completeness check and no validity rule sees it. Only the
improbable repetition of the exact pair gives it away.

On the full file the prevailing wind appears westerly on 43.6% of days. On the
2,244 reliable days it is westerly on **17.7%**.

**2. The record is not the calendar.** 162 days in the span carry no row at all. A
missing row leaves no trace in a missing-value count, because there is no cell to be
empty. Whole months are absent, and the observed-day count per calendar month ranges
from 240 to 310, a **29% spread**.

**3. The file cannot answer the spatial question.** The brief asks for patterns across
cities and countries. There is no city, country or station column. This is a
single-station record, and no spatial comparison is attempted.

## Dashboard: items identified for the next revision

The six indicator cards were verified against the data and are **correct**. Four
statements in the insight panel were written before this analysis was complete.

| Item | Correction |
| :--- | :--- |
| Rainy Days shows 1K | The count is 849; the thousands unit rounds up by 18%. Set the display unit to None |
| February recorded the highest rainfall | June, on both rankings. The Rainfall panel already shows June |
| Humidity peaks during winter months | Peaks in February, which is summer under the southern-hemisphere convention |
| Dominant wind direction: SE | West at 17.7% on the reliable days; SE is 4.5% |

Adding the reliability flag and the season field to the Power BI model resolves three
of the four together.

## Method

Nothing was modified before the problem was measured. The date format was **tested**
rather than assumed: read as `d/m/Y` the column leaves 60% of rows unparsed. The
hemisphere was **established from the data** before seasons were assigned: the warmest
month is January, so December to February is summer, and the northern convention would
invert every seasonal conclusion.

Every monthly figure is reported **twice**, as a raw total and per observed day,
because the months are not equally covered. June is the wettest month on both
rankings, so the conclusion stands; the agreement was established rather than assumed.

The temperature trend is **tested, not asserted**: +1.51 °C per decade, p = 0.020,
r² = 0.62, on the eight complete years. 2012 and 2017 are excluded for insufficient
coverage.

## Running it

Open `Weather_Analysis.ipynb` with the Colab badge at the top and run every cell.
Upload `Weather_Data.csv` when the picker appears.

```bash
pip install pandas numpy matplotlib scipy
python analysis.py
```

## Contents

```
Weather_Analysis/
├── Weather_Analysis.ipynb          Executed notebook, 10 cells, 6 figures
├── Weather_Climate_Report.pdf      Formal report, 11 pages
├── INSIGHTS.md                     Six insights with recommendations
├── analysis.py                     The analysis as a script
├── report.tex                      LaTeX source
├── Weather_Dashboard.pbix          Power BI dashboard
├── WeatherDashboard.json           Power BI theme
├── data/
│   ├── Weather_Data_original.csv   The file as supplied
│   ├── weather_clean.csv           Cleaned, 3,271 rows x 35 columns
│   └── weather_clean_extended.csv  Extended cleaning, 48 columns with anomaly flags
├── figures/                        Six analysis figures plus the dashboard capture
└── results/                        Aggregate tables and findings.json
```
