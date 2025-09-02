# Section 14: Mini Project – Estate Dashboard (Capstone)

## 14.1 Objective
By the end of this project, students will:  
- Build a **Plantation Performance Dashboard** using Python.  
- Integrate multiple datasets (`rainfall.csv`, `block_yields.csv`, `fertilizer.csv`, `labor.csv`, `estate_info.csv`, `estate_dashboard.csv`).  
- Clean, analyze, and visualize data.  
- Present **block-level insights** for management in a single, clear script or notebook.  

---

## 14.2 Project Brief – Business Context
You are the **Estate Data Analyst** for a palm oil plantation. Management wants a **monthly and quarterly performance dashboard** across 4 blocks. The dashboard must answer:  

1. How did rainfall, yield, fertilizer, and labor vary across months?  
2. Which block achieved the **highest productivity**?  
3. Are rainfall and yield correlated?  
4. Did fertilizer application improve yields?  
5. Which block is most efficient (highest Yield per Hectare, best labor productivity)?  

The dashboard must combine:  
- **Tables** (summaries).  
- **Charts** (trends and comparisons).  
- **Insights** (simple conclusions).  

---

## 14.3 Tasks

### 1. Data Import & Cleaning
- Load `estate_dashboard.csv`.  
- Ensure numeric columns (`Yield_tonnes`, `Workers`, `Fertilizer_kg`, `Rainfall_mm`) are correct types.  
- Standardize `Fertilizer_Type` values (MOP, UREA, NPK).  
- Handle missing values appropriately.  

### 2. KPI Calculations
Add new calculated columns:  
- **Yield per Hectare (YPH)** = `Yield_tonnes / Area_ha`  
- **Labor Productivity** = `Tonnes_Harvested / Workers`  
- **Cost per Tonne (simplified)** = `(Workers*1200 + Fertilizer_kg*2.5) / Yield_tonnes`  

### 3. Aggregations & Reports
- **Monthly Summary**: Average rainfall, yield, fertilizer use per block.  
- **Quarterly Summary**: Use groupby (Q1–Q4) to summarize YPH, productivity, and cost/tonne.  
- **Soil Type Comparison**: Join with `estate_info.csv` and compare average YPH across soil types.  

### 4. Visualizations
Create at least 3 charts:  
- Line chart: Rainfall trend per block.  
- Bar chart: Average YPH per block.  
- Scatter plot: Fertilizer vs Yield.  

Optional:  
- Multi-line chart comparing yields of all blocks.  
- Rolling average plot for 3-month yield trends.  

### 5. Insight Extraction
Write **3–5 bullet-point insights** from your dashboard. Example:  
- “Block D has the highest YPH but also the highest cost per tonne.”  
- “Block C shows weak correlation between fertilizer and yield—potential inefficiency.”  
- “Rainfall strongly correlates with yield in Block B.”  

---

## 14.4 Starter Template

```python
import pandas as pd
import matplotlib.pyplot as plt

# 1. Load Data
df = pd.read_csv("estate_dashboard.csv")
info = pd.read_csv("estate_info.csv")

# 2. Clean Data
df["Fertilizer_Type"] = df["Fertilizer_Type"].str.strip().str.upper()
df = df.dropna()

# 3. Add KPIs
df["YPH"] = df["Yield_tonnes"] / df["Area_ha"]
df["Prod"] = df["Tonnes_Harvested"] / df["Workers"]
df["Cost_per_Tonne"] = (df["Workers"]*1200 + df["Fertilizer_kg"]*2.5) / df["Yield_tonnes"]

# 4. Grouping
quarter_map = {
    "Jan":"Q1","Feb":"Q1","Mar":"Q1",
    "Apr":"Q2","May":"Q2","Jun":"Q2",
    "Jul":"Q3","Aug":"Q3","Sep":"Q3",
    "Oct":"Q4","Nov":"Q4","Dec":"Q4"
}
df["Quarter"] = df["Month"].map(quarter_map)
qtr_summary = df.groupby(["Block","Quarter"]).agg({"YPH":"mean","Prod":"mean","Cost_per_Tonne":"mean"})
print(qtr_summary)

# 5. Visualization Examples
# Line chart rainfall trends
for b in df["Block"].unique():
    subset = df[df["Block"]==b]
    plt.plot(subset["Month"], subset["Rainfall_mm"], marker="o", label=b)
plt.title("Rainfall Trend by Block")
plt.xlabel("Month"); plt.ylabel("Rainfall (mm)")
plt.legend(); plt.show()

# Bar chart average YPH per block
avg_yph = df.groupby("Block")["YPH"].mean()
avg_yph.plot(kind="bar", color="green", title="Average YPH per Block")
plt.ylabel("Yield per Hectare"); plt.show()

# Scatter plot fertilizer vs yield
plt.scatter(df["Fertilizer_kg"], df["Yield_tonnes"], c="blue")
plt.title("Fertilizer vs Yield")
plt.xlabel("Fertilizer (kg)"); plt.ylabel("Yield (tonnes)")
plt.show()
```  

---

## 14.5 Reflection Questions
1. Which KPI is most important for estate managers—YPH, productivity, or cost per tonne? Why?  
2. How can the dashboard help detect inefficiencies?  
3. If you had GPS block coordinates, how could you extend this dashboard (hint: geospatial plots)?  

---

## 14.6 Deliverables
- Python script (`estate_dashboard.py`) or Jupyter Notebook.  
- Cleaned dataset (`estate_dashboard_clean.csv`).  
- Visualizations (PNG or inline plots).  
- Summary insights (short report, 3–5 findings).  

---

## 14.7 Section Summary
This capstone pulls together:  
- File handling (loading CSVs).  
- Pandas cleaning & analysis.  
- Statistical exploration.  
- Visualization with Matplotlib.  
- KPI generation for decision-making.  

**End Result:** A working **Estate Performance Dashboard** that managers can use at the end of each month.  
