# Section 12: Visualization with Matplotlib

## 12.1 Why Visualization Matters
Numbers in tables are useful, but **charts tell stories**. Estate managers don’t want to see 500 rows of rainfall and yield—they want a line chart showing whether yields are going up or down.  

**Analogy:** A chart is like a drone photo of your plantation—you see the big picture instantly instead of walking every row.  

---

## 12.2 Introduction to Matplotlib
Matplotlib is Python’s most popular visualization library.  

```python
import matplotlib.pyplot as plt
```

- `plt.plot()` → line chart  
- `plt.bar()` → bar chart  
- `plt.scatter()` → scatter plot  
- `plt.show()` → display chart  

---

## 12.3 Simple Line Chart – Rainfall Trends
```python
import pandas as pd
import matplotlib.pyplot as plt

df = pd.read_csv("rainfall.csv")
block_a = df[df["Block"] == "A"]

plt.plot(block_a["Month"], block_a["Rainfall_mm"], marker="o")
plt.title("Rainfall Trend – Block A")
plt.xlabel("Month")
plt.ylabel("Rainfall (mm)")
plt.show()
```

👉 Managers instantly see **wet vs dry months**.  

---

## 12.4 Bar Chart – Yield by Block
```python
df = pd.read_csv("block_yields.csv")
avg_yield = df.groupby("Block")["Yield_tonnes"].mean()

plt.bar(avg_yield.index, avg_yield.values, color="green")
plt.title("Average Yield per Block")
plt.xlabel("Block")
plt.ylabel("Yield (tonnes)")
plt.show()
```

---

## 12.5 Scatter Plot – Rainfall vs Yield
```python
df = pd.read_csv("estate_dashboard.csv")

plt.scatter(df["Rainfall_mm"], df["Yield_tonnes"], color="blue")
plt.title("Rainfall vs Yield")
plt.xlabel("Rainfall (mm)")
plt.ylabel("Yield (tonnes)")
plt.show()
```

👉 Helps check correlation visually.  

---

## 12.6 Adding Labels, Legends & Styles
```python
block_b = df[df["Block"] == "B"]

plt.plot(block_a["Month"], block_a["Yield_tonnes"], label="Block A")
plt.plot(block_b["Month"], block_b["Yield_tonnes"], label="Block B")
plt.title("Yield Trend Comparison")
plt.xlabel("Month")
plt.ylabel("Yield (tonnes)")
plt.legend()
plt.grid(True)
plt.show()
```

---

## 12.7 Plantation Case Study – Dashboard Charts
Using **estate_dashboard.csv**:  
1. Plot rainfall trends for each block.  
2. Compare fertilizer use in bar charts.  
3. Plot yield vs workers productivity scatter plots.  

---

## 12.8 Reflection Questions
1. Why is a scatter plot more useful than a table when checking correlation?  
2. How would you explain rainfall trends to a manager using a line chart?  
3. What mistakes could happen if charts are misleading (wrong scale, missing labels)?  

---

## 12.9 Practice Exercises

**Exercise 12.1 – Line Chart**  
- Plot rainfall over the year for Block D.  

**Exercise 12.2 – Bar Chart**  
- Compare total fertilizer usage across all blocks.  

**Exercise 12.3 – Scatter Plot**  
- Plot Workers vs Tonnes_Harvested to check productivity patterns.  

**Exercise 12.4 – Multiple Lines**  
- Plot yield trends for Blocks A, B, C, D on the same chart.  

**Exercise 12.5 – Challenge**  
- Create a small **Estate Dashboard** with 3 subplots:  
  1. Rainfall trend (line chart)  
  2. Average yield per block (bar chart)  
  3. Rainfall vs Yield (scatter plot)  

---

## 12.10 Section Summary
- Matplotlib is the workhorse of Python visualization.  
- Line charts show trends, bar charts show comparisons, scatter plots show relationships.  
- Adding labels, titles, and legends makes charts management-friendly.  
- Plantation dashboards can mix multiple charts to tell a full story.  

**Take-home Challenge:**  
Using `estate_dashboard.csv`:  
1. Create a line chart showing rainfall and yield for Block B.  
2. Create a bar chart comparing average yield per hectare across blocks.  
3. Create a scatter plot of fertilizer use vs yield.  
