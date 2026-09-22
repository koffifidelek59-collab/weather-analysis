# Key Insights

**Weather and Climate Pattern Analysis** &middot; 3,271 daily observations, 2008 to 2017
KOUAME Koffi Fidèle &middot; Data Analysis Internship

---

## Headline indicators

| Indicator | Value |
| :--- | ---: |
| Observations | 3,271 days |
| Mean temperature | 18.94 °C |
| Highest / lowest temperature | 45.8 / 4.3 °C |
| Mean humidity | 61.47% |
| Mean wind speed | 17.19 km/h |
| Total rainfall | 10,932 mm |
| Rainy days | 849 (26.0%) |
| Mean pressure | 1017.2 hPa |
| Mean sunshine | 7.17 hours |

---

## 1. Nearly a third of the wind record is a placeholder

The pair **west, 41 km/h** occurs on **1,027 days**, 31.4% of the file and
**32 times** the next most frequent direction-and-speed combination. It covers
**every single day of 2008 and 2009** and 80% of 2010, then all but disappears.

This is a backfill of the period before the gust instrument began reporting.

**Why nothing else catches it.** West is a legal direction, 41 km/h is inside the
observed range of 17 to 96, and the cells are populated. A completeness audit sees
nothing, a validity rule sees nothing. Only the improbable repetition of the exact
pair gives it away.

**What it changes.** On the full file the prevailing wind appears westerly on 43.6%
of days. On the 2,244 reliable days it is westerly on
17.7%, ahead of south-south-east at 10.7%.

**Recommendation.** Treat wind gust as unusable before 2011. Add a reliability flag
to the table so the exclusion is visible rather than tacit, and run a constant-pair
test on every instrument-derived column before publishing anything from it.

## 2. The record is not the calendar

**162 calendar days** in the span carry no row at all, 4.7% of the period. A missing
row leaves no trace in a missing-value count, because there is no cell to be empty.

Whole months are absent: December 2012, April 2011, February 2013. The observed-day
count per calendar month ranges from 240 to 310, a **29% spread**.

**What it changes.** Every monthly total compares samples of unequal size. Reported
both ways, June is the wettest month and September the driest on the raw total **and**
on the per-day rate. The rankings agree, so the conclusion stands, but that agreement
was established rather than assumed.

**Recommendation.** Publish rainfall as millimetres per observed day alongside the
total, and show the observed-day count beside any monthly figure.

## 3. The seasonal signal is southern hemisphere, and the sign matters

The warmest month is **Jan** and the coolest is **Jul**.
Summer averages 23.25 °C against 14.18 °C in winter.

Applying the northern convention would place the hottest quarter in winter and invert
every seasonal statement. The dashboard's humidity insight is exactly this error:
humidity peaks in **Feb** at 66.7%, and February was read as winter.

**Recommendation.** State the hemisphere convention on the dashboard. One line
removes an entire class of misreading.

## 4. Warming of 1.51 °C per decade, significant but short

The trend across the 8 complete years is **+1.51 °C per decade**,
p = 0.0198, r² = 0.623. The slope is unlikely to be noise.

It is also fitted on 8 annual points spanning nine years, at one station.
A decade is short for a climate statement.

**Recommendation.** Report the slope with its p-value and its sample size, never the
slope alone. Describe it as a property of this record, not as a projection.

## 5. Rain and warmth are in opposition here

Autumn delivers 4.00 mm per observed day and winter 3.63, against 2.31 in spring.
June alone receives **3.4 times** what September receives, while January is the
warmest month.

The wet season and the warm season do not coincide, which is the single most useful
fact in the record for anyone planning around it.

## 6. Cloud and sunshine are one measurement taken twice

They correlate at **-0.75**,
describing the same physical state from opposite directions. A model using both gains
little from the second.

The strongest relationship between genuinely distinct quantities is temperature
against evaporation at +0.57.

**Recommendation.** Keep one of the pair, and prefer sunshine: it is measured on a
continuous scale rather than in eight steps.

---

## Dashboard: items identified for the next revision

The six indicator cards were verified against the data and are **correct**. Four
statements in the insight panel were written before this analysis was complete and do
not match the findings. Each has a straightforward fix.

| Item | Correction |
| :--- | :--- |
| Rainy Days card shows 1K | The count is 849. The card applies a thousands abbreviation to a three-digit number, rounding up by 18%. Set the display unit to None |
| February recorded the highest rainfall | June, on both rankings, 5.90 mm per observed day against 4.32. The Rainfall Analysis panel already shows June, so the two will be brought into agreement |
| Humidity peaks during winter months | Peaks in February at 66.7%, which is summer under the southern-hemisphere convention |
| Dominant wind direction: SE | West leads at 17.7% on the reliable days; SE is 4.5%. To be recomputed once the placeholder flag is added to the model |

Two statements are confirmed and need no change: summer is the warmest season, and the
temperature trend is upward. The analysis quantifies the second at +1.51 °C per decade,
which the dashboard can now state rather than imply.

**The underlying cause of three of the four.** The wind placeholder and the hemisphere
convention were both established in this analysis, after the dashboard was built.
Adding the reliability flag and the season field to the Power BI model resolves the
wind and humidity items together.

## What this data cannot answer

**Anything spatial.** The brief describes patterns across cities and countries. The
file has no city, country or station column. It is a single-station record.

**Wind before 2011**, for the reason in insight 1.

**Long-term climate.** Nine years at one station cannot support a climate projection.

**Causation.** Nothing here establishes why the measures covary.
