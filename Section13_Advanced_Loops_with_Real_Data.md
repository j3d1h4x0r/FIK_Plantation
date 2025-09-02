# Section 13: Advanced Loops with Real Data

## 13.1 Why “Advanced Loops”? (And When *Not* to Loop)
Loops are powerful, but with **real datasets** (thousands of rows), looping row‑by‑row can be slow and error‑prone.  
Pandas gives us **vectorized operations**, **groupby**, and **apply** — these are faster and usually clearer.

**Rule of thumb:**  
- If you’re iterating just to compute per‑row formulas, **prefer vectorized columns**.  
- If you’re summarizing by Block/Month/Quarter, **prefer `groupby` / `pivot_table`**.  
- Use `for` loops **only** when you must perform custom logic that can’t be expressed with vectorized ops.

---

## 13.2 Dataset Setup
We’ll use the combined capstone dataset from Day 2:
- `estate_dashboard.csv` with columns:  
  `Month, Block, Rainfall_mm, Yield_tonnes, Area_ha, Workers, Fertilizer_kg, Tonnes_Harvested, Fertilizer_Type`

```python
import pandas as pd

df = pd.read_csv("estate_dashboard.csv")
df.head()
```

---

## 13.3 Vectorized KPIs (No Loops)
Compute **Yield per Hectare (YPH)** and **Labor Productivity** using vectorized column math.

```python
df["YPH"] = df["Yield_tonnes"] / df["Area_ha"]
df["Prod_tonnes_per_worker"] = df["Tonnes_Harvested"] / df["Workers"]
df[["Block","Month","YPH","Prod_tonnes_per_worker"]].head()
```

This is both **faster** and **cleaner** than looping row‑by‑row.

---

## 13.4 Smart Iteration: `itertuples()` > `iterrows()`
Sometimes you do need to iterate. Prefer `itertuples()` — it’s faster and gives attribute‑style access.

```python
for row in df.itertuples(index=False):
    # Example: flag possible anomalies inline
    if (row.Rainfall_mm < 180) and (row.Yield_tonnes > 30):
        print(f"Check: Block {row.Block} in {row.Month} had high yield under low rain.")
```

Use this style only for **custom conditions** you can’t vectorize easily.

---

## 13.5 Grouping & Aggregating (Quarterly KPIs)
Let’s compute **quarterly** summaries per block. First, map Month→Quarter.

```python
month_to_q = {
    "Jan":"Q1","Feb":"Q1","Mar":"Q1",
    "Apr":"Q2","May":"Q2","Jun":"Q2",
    "Jul":"Q3","Aug":"Q3","Sep":"Q3",
    "Oct":"Q4","Nov":"Q4","Dec":"Q4",
}
df["Quarter"] = df["Month"].map(month_to_q)

# Vectorized KPIs first (if not already computed)
df["YPH"] = df["Yield_tonnes"] / df["Area_ha"]
df["Prod_tonnes_per_worker"] = df["Tonnes_Harvested"] / df["Workers"]

qtr = (
    df.groupby(["Block","Quarter"], as_index=False)
      .agg(
          Yield_tonnes_sum=("Yield_tonnes","sum"),
          Area_ha_mean=("Area_ha","mean"),
          Workers_mean=("Workers","mean"),
          Rainfall_mm_sum=("Rainfall_mm","sum"),
          Fertilizer_kg_sum=("Fertilizer_kg","sum"),
          YPH_avg=("YPH","mean"),
          Prod_avg=("Prod_tonnes_per_worker","mean")
      )
      .sort_values(["Block","Quarter"])
)
qtr.head()
```

**Notes:**  
- We keep `Area_ha_mean` because area is static; mean = value.  
- `mean` vs `sum`: choose what makes sense for the KPI.

---

## 13.6 Pivot Tables (Report‑friendly Tables)
Pivot tables rearrange summaries into matrix form.

```python
pivot_yph = pd.pivot_table(
    df, values="YPH", index="Block", columns="Month", aggfunc="mean"
)
pivot_yph
```

Great for management reports (Blocks as rows, Months as columns).

---

## 13.7 Multi-Condition Labels with `apply`
Complex rules can be encoded with `apply` across rows. (Still slower than vectorization, but simpler than many nested loops.)

```python
def classify_row(r):
    score = 0
    if r["YPH"] >= 2.3: score += 1
    if r["Prod_tonnes_per_worker"] >= 2.0: score += 1
    if r["Rainfall_mm"] >= 200: score += 1
    return {0:"Poor", 1:"Okay", 2:"Good", 3:"Excellent"}[score]

df["Perf_Label"] = df.apply(classify_row, axis=1)
df[["Block","Month","YPH","Prod_tonnes_per_worker","Rainfall_mm","Perf_Label"]].head()
```

If performance matters, convert rules into **vectorized boolean masks** instead.

---

## 13.8 Joining Master Data (Merges)
Bring in static information like soil type (`estate_info.csv`).

```python
info = pd.read_csv("estate_info.csv")
df2 = df.merge(info[["Block","Soil_Type"]], on="Block", how="left")
df2[["Block","Month","Soil_Type","YPH"]].head()
```

Now you can compare KPIs by soil type.

---

## 13.9 Rolling Metrics (3‑Month Moving Average per Block)
A moving average smooths noisy monthly series. We need a sortable month index:

```python
order = ["Jan","Feb","Mar","Apr","May","Jun","Jul","Aug","Sep","Oct","Nov","Dec"]
df["Month_idx"] = df["Month"].apply(order.index)

df = df.sort_values(["Block","Month_idx"])
df["YPH_MA3"] = df.groupby("Block")["YPH"].transform(lambda s: s.rolling(3, min_periods=1).mean())
df[["Block","Month","YPH","YPH_MA3"]].head(15)
```

---

## 13.10 From For‑Loops to Groupby: A Mindset Shift
**Instead of:**

```python
# Slow anti-pattern
totals = {}
for b in df["Block"].unique():
    subset = df[df["Block"] == b]
    totals[b] = subset["Yield_tonnes"].sum()
```

**Prefer:**

```python
totals = df.groupby("Block")["Yield_tonnes"].sum()
```

Cleaner. Faster. Fewer bugs.

---

## 13.11 Reflection Questions
1. When is a plain `for` loop the right tool with DataFrames?  
2. Why do `groupby` and `pivot_table` scale better than nested loops?  
3. What are the trade‑offs between `apply` and pure vectorization?  

---

## 13.12 Practice Exercises

**Exercise 13.1 – Quarterly Productivity**  
- Using `estate_dashboard.csv`, compute **quarterly average productivity** (`Tonnes_Harvested / Workers`) for each block using `groupby`.  
- Output a table: `Block, Quarter, Prod_avg`.

**Exercise 13.2 – Pivot KPIs**  
- Create a pivot table of **average YPH** with `Block` as rows and `Month` as columns.  
- Identify which block‑month combos fall below 2.0 YPH.

**Exercise 13.3 – Soil Type Join**  
- Merge in `estate_info.csv` to attach `Soil_Type`.  
- Compute **average YPH per Soil_Type** and discuss differences.

**Exercise 13.4 – Rolling Trend**  
- Compute a **3‑month moving average** of YPH per block.  
- Which block shows the most consistent improvement across the year?

**Exercise 13.5 – Challenge: Vectorize Your Rules**  
- Create labels: “Gold” if `YPH ≥ 2.5` **and** `Prod ≥ 2.2`; “Silver” if either condition holds; otherwise “Bronze”.  
- Implement **without** `apply` (use boolean masks and `.loc`).

---

## 13.13 Section Summary
- Prefer **vectorized math** and **groupby** to loops for speed and clarity.  
- Use `itertuples()` for unavoidable row‑wise custom logic.  
- `pivot_table`, `merge`, and `rolling` unlock real‑world analysis patterns.  
- Quarterly summaries, soil comparisons, and moving averages make your analytics **management‑ready**.

**Take‑home Challenge:**  
Build a script that:  
1) Adds `YPH`, `Prod`, `Quarter`, `Month_idx`.  
2) Produces a quarterly summary per block (YPH_avg, Prod_avg, Rainfall_sum).  
3) Adds a 3‑month rolling YPH and finds the best consecutive quarter for each block.  
4) Saves two outputs: `quarterly_summary.csv` and `rolling_yph.csv`.
