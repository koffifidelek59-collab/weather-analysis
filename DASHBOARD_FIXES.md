# Power BI: corrections to apply

**Weather Analytics Dashboard** &middot; menu labels in English, as in your installation

Ordered by impact. The first three change what the charts say; the rest are wording.

---

## 1. Three time series are not in time order

This is the most visible defect, and the most costly: a line chart whose x-axis is out
of sequence shows a trend that does not exist.

**Temperature Trend Over Time** currently reads 2008, 2012, 2011, 2010, 2009, 2015,
2013, 2014, 2016, 2017. The line rises and falls according to the sort, not according
to the years.

**Monthly Summary** reads Jan, Feb, Mar, Dec, Nov, Apr, Oct, Sep, May, Aug, Jun, Jul.

**Humidity Analysis** reads Feb, Mar, Jun, Apr, Jan, Dec, May, Nov, Jul, Oct, Aug, Sep.

### The fix for the year axis

Click the chart, then the three dots at its top right, **Sort axis**, choose **Year**,
then **Sort ascending**.

### The fix for the month axis

Sorting by the month name sorts alphabetically, so it must be sorted by a number.

1. In **Table view**, select your date table.
2. **Table tools**, **New column**:
   ```
   MonthNumber = MONTH('Weather'[Date])
   ```
3. Select the **MonthName** column, then **Column tools**, **Sort by column**, choose
   **MonthNumber**.
4. Every chart using MonthName now orders January to December automatically.

If your model uses `MonthName` from the cleaned CSV, the column `Month` already holds
the number and step 2 can be skipped.

---

## 2. Rainy Days shows 1K instead of 849

The card applies a thousands abbreviation to a three-digit number, which rounds 849 up
to 1000 and overstates the count by 18%.

Click the card, **Format visual**, **Callout value**, set **Display units** to
**None**, and **Value decimal places** to **0**.

Check the other five cards while you are there: Total Rainfall at 10.93K is correct in
substance but reads better as **10,932 mm** with the unit shown.

---

## 3. The page gives three different answers about wind

| Where | What it shows | Which column it measures |
| :--- | :--- | :--- |
| Wind Analysis panel | Dominant Wind **E** | `WindDir3pm`, the 3 pm direction |
| Key Insights | Dominant wind direction **SE** | not reproducible from any column |
| Wind rose | the gust rose | `WindGustDir` |

**The measurement each one uses is different, so the reader cannot tell which is the
answer.** Pick one definition and label it.

The recommendation is to use the **gust direction on reliable days**, because that is
what a wind rose conventionally shows:

1. Add a column to the model:
   ```
   WindGust_Reliable = IF('Weather'[WindGustDir] = "W" && 'Weather'[WindGustSpeed] = 41, 0, 1)
   ```
2. Add it to the page filters, set to **1**.
3. Rename the card **Dominant gust direction (reliable days)**.

It then reads **W, 17.7%**, and the wind rose beside it agrees with it.

**Max Wind Speed 50.00 is correct** as the maximum of the daily mean. Label it
**Max daily mean wind speed** so it is not read as the strongest gust, which is 96 km/h.

---

## 4. Four statements in Key Insights

Replace the panel text with the following. Two of the five current statements are
correct and are kept.

| Current | Replace with |
| :--- | :--- |
| Summer (Dec-Feb) is the warmest season | **keep**, it is correct |
| Temperature shows a slight increase | **Temperature rises 1.51 °C per decade (p = 0.020)** |
| February recorded the highest rainfall | **June is the wettest month, 5.90 mm per observed day** |
| Humidity peaks during winter months | **Humidity peaks in February at 66.7%, the height of summer** |
| Dominant wind direction: SE | **Prevailing gust is westerly on 17.7% of reliable days** |

The rainfall one matters most: your own **Rainfall Analysis** panel already shows June
as the wettest month, so the page currently contradicts itself on the same screen.

---

## 5. Two additions worth making

**Show the coverage.** 162 calendar days carry no observation, and the observed-day
count per month ranges from 240 to 310. Add a small card:

```
Observed days = COUNTROWS('Weather')
Coverage = DIVIDE(COUNTROWS('Weather'), DATEDIFF(MIN('Weather'[Date]), MAX('Weather'[Date]), DAY) + 1)
```

Place it near the Rainfall Analysis panel, because that is the chart the gaps affect.

**Normalise the rainfall chart.** Replace the total with a per-day rate so the months
are comparable:

```
Rainfall per observed day = DIVIDE(SUM('Weather'[Rainfall]), COUNTROWS('Weather'))
```

The ranking does not change here, June stays first, but the chart becomes defensible
if anyone asks whether the months are equally covered.

---

## 6. One line to add to the page

Put a text box in a corner:

> Southern hemisphere: December to February is summer.

It costs one line and prevents the humidity misreading from recurring.

---

## Order of work

1. The three sort fixes, ten minutes, and they change what the charts say.
2. The Rainy Days display unit, one minute.
3. The Key Insights text, five minutes.
4. The wind reliability filter and label, fifteen minutes.
5. The coverage card and the normalised rainfall measure, if time allows.
