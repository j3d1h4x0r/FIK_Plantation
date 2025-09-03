# Section 20: Visualization for Reporting

## 20.1 Why Reporting Matters
You’ve done the hard work of cleaning, merging, and analyzing data. But managers don’t want to read Python code or DataFrames — they want clear visuals and summaries that help with decision-making.  

**Analogy:** Data analysis is the chef cooking a meal; reporting is plating it beautifully for the diner.  

---

## 20.2 Principles of Good Reporting Visuals
1. **Clarity** – Every axis must be labeled, every chart titled.  
2. **Simplicity** – Use the simplest chart that communicates the message.  
3. **Consistency** – Keep colors and scales uniform across charts.  
4. **Insight-driven** – Each chart should answer a management question.  

---

## 20.3 Management-Ready Bar & Line Charts

### Example: Yield vs Fertilizer by Block
```python
import pandas as pd
import matplotlib.pyplot as plt

df = pd.read_csv("estate_dashboard.csv")

avg = df.groupby("Block")[["Fertilizer_kg","Yield_tonnes"]].mean()

fig, ax1 = plt.subplots()

ax1.bar(avg.index, avg["Fertilizer_kg"], color="orange", alpha=0.6, label="Fertilizer (kg)")
ax1.set_ylabel("Fertilizer (kg)", color="orange")

ax2 = ax1.twinx()
ax2.plot(avg.index, avg["Yield_tonnes"], marker="o", color="green", label="Yield (tonnes)")
ax2.set_ylabel("Yield (tonnes)", color="green")

plt.title("Average Fertilizer vs Yield by Block")
plt.show()
```
👉 A **dual-axis chart** shows fertilizer input vs yield output in one view.  

---

## 20.4 Comparative Dashboards

### Example: Yield Trends for All Blocks
```python
for b in df["Block"].unique():
    subset = df[df["Block"]==b]
    plt.plot(subset["Month"], subset["Yield_tonnes"], marker="o", label=f"Block {b}")

plt.title("Monthly Yield Trends by Block")
plt.xlabel("Month"); plt.ylabel("Yield (tonnes)")
plt.legend(); plt.grid(True)
plt.show()
```
👉 Managers can instantly see which block is stable, which is volatile.  

---

## 20.5 Scatter Plots with Regression Lines
```python
import seaborn as sns

sns.regplot(data=df, x="Rainfall_mm", y="Yield_tonnes")
plt.title("Rainfall vs Yield with Regression Line")
plt.show()
```
👉 Adds a **trend line** to show direction and strength of the relationship.  

---

## 20.6 Case Study – Executive Dashboard
Your final report to management should include:  
1. **Key KPIs** – Yield per Hectare, Productivity per Worker.  
2. **Input vs Output Charts** – Fertilizer vs Yield, Rainfall vs Yield.  
3. **Block Comparisons** – Ranking blocks by efficiency.  
4. **Trend Lines** – Seasonal patterns across months.  
5. **Insights Section** – Bullet-point conclusions.  

---

## 20.7 Reflection Questions
1. Why should you avoid overly complex charts in management reports?  
2. How can consistent colors (e.g., green = yield, blue = rainfall) improve readability?  
3. Why include both visuals **and** bullet-point insights?  

---

## 20.8 Practice Exercises

**Exercise 20.1 – Dual-Axis Chart**  
- Create a bar + line chart of Fertilizer vs Yield per block.  

**Exercise 20.2 – Multi-Line Trend**  
- Plot monthly yield trends for all blocks on the same chart.  

**Exercise 20.3 – Regression Scatter**  
- Add a regression line to Rainfall vs Yield.  

**Exercise 20.4 – Challenge**  
- Build a **3-panel dashboard** with:  
  - Panel 1: Rainfall vs Yield scatter + regression.  
  - Panel 2: Yield per Block (bar chart).  
  - Panel 3: Productivity per Worker (line chart).  

---

## 20.9 Section Summary
- Reporting is about **communication**, not just analysis.  
- Use dual-axis, trend, and regression charts to simplify insights.  
- Dashboards combine multiple views into a single management report.  
- Always include **visuals + narrative insights** for maximum impact.  

**Take-home Challenge:**  
Build a **management-ready dashboard** using `estate_dashboard.csv` that includes:  
1. Yield per Hectare across blocks.  
2. Fertilizer vs Yield comparison.  
3. Rainfall vs Yield scatter with regression.  
4. Two insights for management: “Which block is most efficient?” and “Is fertilizer investment paying off?”  
