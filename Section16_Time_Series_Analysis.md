# Section 16: Time-Series Analysis (Basic Forecasting)

## 16.1 Why Time-Series?
Plantation data is **temporal** — rainfall, yields, labor, and fertilizer are tracked month by month. Looking at averages alone hides **seasonality** and **trends**.  

**Analogy:** Instead of looking at a single photograph of your estate, time-series analysis is like flipping through a year-long photo album to see changes over time.  

---

## 16.2 Preparing Time Data in Pandas

### Example: Converting Months to Time Index
```python
import pandas as pd

df = pd.read_csv("estate_dashboard.csv")

# Convert Month names into an ordered categorical type
months = ["Jan","Feb","Mar","Apr","May","Jun","Jul","Aug","Sep","Oct","Nov","Dec"]
df["Month"] = pd.Categorical(df["Month"], categories=months, ordered=True)

# Sort the DataFrame
df = df.sort_values(["Block","Month"])
print(df.head())
```
👉 Ensures Jan → Dec ordering, not alphabetical (Apr before Feb).  

---

## 16.3 Plotting Trends Over Time

### Example: Rainfall Trends per Block
```python
import matplotlib.pyplot as plt

for b in df["Block"].unique():
    subset = df[df["Block"]==b]
    plt.plot(subset["Month"], subset["Rainfall_mm"], marker="o", label=b)

plt.title("Rainfall Trend by Block")
plt.xlabel("Month"); plt.ylabel("Rainfall (mm)")
plt.legend(); plt.show()
```

---

## 16.4 Moving Averages – Smoothing Noise
Yields often fluctuate due to short-term effects. A **moving average** shows long-term trend.  

```python
df["Yield_MA3"] = df.groupby("Block")["Yield_tonnes"].transform(
    lambda s: s.rolling(3, min_periods=1).mean()
)

print(df[["Block","Month","Yield_tonnes","Yield_MA3"]].head(12))
```
👉 Smooths out sudden spikes/dips, revealing trend direction.  

---

## 16.5 Seasonal Patterns

Example: Quarterly yield averages.  

```python
quarter_map = {
    "Jan":"Q1","Feb":"Q1","Mar":"Q1",
    "Apr":"Q2","May":"Q2","Jun":"Q2",
    "Jul":"Q3","Aug":"Q3","Sep":"Q3",
    "Oct":"Q4","Nov":"Q4","Dec":"Q4",
}
df["Quarter"] = df["Month"].map(quarter_map)

qtr = df.groupby(["Block","Quarter"])["Yield_tonnes"].mean()
print(qtr)
```

---

## 16.6 Basic Forecasting – Next Year Projection
A simple way: Use the **average of past quarters** to predict next year.  

```python
forecast = df.groupby(["Block","Quarter"])["Yield_tonnes"].mean().reset_index()
forecast.rename(columns={"Yield_tonnes":"Forecast_Yield"}, inplace=True)
print(forecast)
```
👉 This gives a **baseline forecast** for each block, per quarter.  

---

## 16.7 Plantation Case Study – Rainfall Impact
Question: *If rainfall increases by 10% next year, how much yield can we expect?*  

```python
corr = df[["Rainfall_mm","Yield_tonnes"]].corr().iloc[0,1]
avg_yield = df["Yield_tonnes"].mean()
impact = avg_yield * (1 + 0.10*corr)

print("Projected Yield if Rainfall +10%:", impact)
```

---

## 16.8 Reflection Questions
1. Why is sorting months critical before time-series analysis?  
2. What does a 3-month moving average reveal that raw yields cannot?  
3. Why is correlation-based forecasting risky in plantations?  

---

## 16.9 Practice Exercises

**Exercise 16.1 – Time Ordering**  
- Ensure `rainfall.csv` months are ordered Jan–Dec.  

**Exercise 16.2 – Moving Average**  
- Compute a 3-month rolling average for `Yield_tonnes` in Block B.  

**Exercise 16.3 – Seasonal Summary**  
- Compute average rainfall per quarter for each block.  

**Exercise 16.4 – Trend Plot**  
- Plot yield trends for all blocks across the year.  

**Exercise 16.5 – Challenge**  
- Forecast next year’s quarterly yields by averaging historical quarters.  
- Compare forecasted vs actual yields if you have 2 years of data (simulate by duplicating data).  

---

## 16.10 Section Summary
- Plantation data is inherently **time-based**.  
- Sorting months ensures correct sequence.  
- Moving averages smooth noise, revealing real trends.  
- Quarterly summaries highlight seasonal cycles.  
- Simple forecasting can guide planning, though more advanced models may be needed for precision.  

**Take-home Challenge:**  
Using `estate_dashboard.csv`:  
1. Create a 12-month line chart of rainfall and yield per block.  
2. Compute 3-month moving average yields.  
3. Produce a simple quarterly forecast for next year.  
4. Write 2 insights about seasonal effects on yields.  
