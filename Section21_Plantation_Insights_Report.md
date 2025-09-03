# Section 21: Capstone – Plantation Insights Report

## 21.1 Objective
By the end of this project, students will:  
- Build a **full analysis report** combining cleaning, merging, statistical testing, forecasting, and visualization.  
- Generate **data-backed recommendations** for plantation management.  
- Present both **code outputs** and **executive-level insights**.  

---

## 21.2 Business Scenario
You are the Data Analyst for a palm oil estate. Management is debating whether to **increase fertilizer budget** or **hire more workers** for next year.  

They want you to prepare a **report** with:  
1. Yield and productivity trends.  
2. Fertilizer efficiency analysis.  
3. Labor productivity insights.  
4. Forecasted yields for the next quarter.  
5. A recommendation: invest more in fertilizer, labor, or neither.  

---

## 21.3 Tasks

### Step 1 – Data Preparation
- Merge `estate_dashboard.csv` with rainfall, labor, fertilizer, and soil data.  
- Clean and standardize columns (Month ordering, Fertilizer_Type categories).  
- Add calculated KPIs:  
  - Yield per Hectare (YPH)  
  - Productivity per Worker  
  - Fertilizer Efficiency (Yield per kg Fertilizer)  

### Step 2 – Exploratory Analysis
- Pivot table: average YPH by block and quarter.  
- Crosstab: fertilizer type usage across blocks.  
- Scatter plot: Rainfall vs Yield.  

### Step 3 – Statistical Testing
- Test if fertilizer type significantly affects yield (t-test).  
- Test if blocks with >25 workers have significantly higher productivity.  

### Step 4 – Time-Series Forecast
- Compute 3-month moving averages of yield per block.  
- Forecast next quarter’s yields using historical quarterly means.  

### Step 5 – Machine Learning Model
- Build a regression model predicting yield from Rainfall, Fertilizer, and Workers.  
- Interpret coefficients to see which factor matters most.  

### Step 6 – Final Report (Executive Style)
1. **Executive Summary** (1 page)  
   - High-level findings and recommendations.  

2. **Data Overview** (tables & pivots)  
   - Monthly/quarterly KPIs.  

3. **Statistical Evidence**  
   - Fertilizer and labor impact significance tests.  

4. **Forecasts & Predictions**  
   - Next quarter’s expected yields.  

5. **Visual Dashboards**  
   - Charts: Fertilizer vs Yield, Rainfall trends, Block comparisons.  

6. **Recommendations**  
   - Actionable advice for resource allocation.  

---

## 21.4 Starter Template
```python
import pandas as pd
import matplotlib.pyplot as plt
from scipy import stats
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression

# 1. Load and merge datasets
df = pd.read_csv("estate_dashboard.csv")
soil = pd.read_csv("estate_info.csv")
df = df.merge(soil, on="Block", how="left")

# 2. Add KPIs
df["YPH"] = df["Yield_tonnes"] / df["Area_ha"]
df["Prod_per_worker"] = df["Yield_tonnes"] / df["Workers"]
df["Fert_eff"] = df["Yield_tonnes"] / df["Fertilizer_kg"]

# 3. Statistical test (MOP vs UREA yields)
mop = df[df["Fertilizer_Type"]=="MOP"]["Yield_tonnes"]
urea = df[df["Fertilizer_Type"]=="UREA"]["Yield_tonnes"]
t_stat, p_val = stats.ttest_ind(mop, urea, equal_var=False)
print("Fertilizer t-test p-value:", p_val)

# 4. Simple forecast (average by quarter)
quarter_map = {"Jan":"Q1","Feb":"Q1","Mar":"Q1",
               "Apr":"Q2","May":"Q2","Jun":"Q2",
               "Jul":"Q3","Aug":"Q3","Sep":"Q3",
               "Oct":"Q4","Nov":"Q4","Dec":"Q4"}
df["Quarter"] = df["Month"].map(quarter_map)
forecast = df.groupby(["Block","Quarter"])["Yield_tonnes"].mean()
print(forecast)

# 5. Regression model
X = df[["Rainfall_mm","Fertilizer_kg","Workers"]]
y = df["Yield_tonnes"]
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
model = LinearRegression().fit(X_train, y_train)
print("Coefficients:", model.coef_)
```  

---

## 21.5 Reflection Questions
1. Which KPI (YPH, productivity, fertilizer efficiency) is most important for management?  
2. How would you explain statistical results (like p-values) in plain terms to a non-technical audience?  
3. What risks exist if management bases decisions only on forecasts without testing assumptions?  

---

## 21.6 Deliverables
- Python script or Jupyter notebook.  
- Visualizations (PNG or inline).  
- Statistical test results (t-test/chi-square).  
- Forecast tables and regression outputs.  
- Final report (PowerPoint or PDF) with recommendations.  

---

## 21.7 Section Summary
This capstone simulates **real-world reporting**:  
- You merge, clean, and explore multi-source data.  
- You test hypotheses with statistics.  
- You forecast and build predictive models.  
- You present insights with visuals and bullet-point recommendations.  

**End Result:** A professional-grade **Plantation Insights Report** that could be shown to management for strategic decisions.  
