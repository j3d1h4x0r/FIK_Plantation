# Section 15: Advanced Data Exploration

## 15.1 Why Advanced Exploration?
So far, you’ve summarized single columns (averages, correlations). But in real plantation analysis:  
- Yield depends on **rainfall + fertilizer + labor** together.  
- Management wants comparisons across **blocks, months, and soil types** at the same time.  

Advanced exploration tools like **crosstabs** and **pivot tables** let you handle this multi-dimensional view.  

**Analogy:** Instead of flipping through one ledger at a time, you spread multiple ledgers on a big table, comparing side-by-side.  

---

## 15.2 Crosstabs in Pandas

### Example: Fertilizer Type vs Block Usage
```python
import pandas as pd

df = pd.read_csv("fertilizer.csv")

crosstab = pd.crosstab(df["Block"], df["Fertilizer_Type"])
print(crosstab)
```

👉 Output shows how many times each block used MOP, UREA, or NPK.  

---

## 15.3 Pivot Tables – The Swiss Army Knife

### Example: Average Yield by Block and Month
```python
df = pd.read_csv("block_yields.csv")

pivot = pd.pivot_table(
    df,
    values="Yield_tonnes",
    index="Block",
    columns="Month",
    aggfunc="mean"
)
print(pivot)
```

👉 Managers instantly see seasonal yield differences per block.  

---

## 15.4 Multi-variable Aggregation

### Example: Rainfall + Yield Relationship by Quarter
```python
df = pd.read_csv("estate_dashboard.csv")

quarter_map = {
    "Jan":"Q1","Feb":"Q1","Mar":"Q1",
    "Apr":"Q2","May":"Q2","Jun":"Q2",
    "Jul":"Q3","Aug":"Q3","Sep":"Q3",
    "Oct":"Q4","Nov":"Q4","Dec":"Q4",
}
df["Quarter"] = df["Month"].map(quarter_map)

pivot = pd.pivot_table(
    df,
    values=["Rainfall_mm","Yield_tonnes"],
    index="Block",
    columns="Quarter",
    aggfunc="mean"
)
print(pivot)
```

👉 Now you can compare rainfall vs yield side by side across quarters.  

---

## 15.5 Plantation Case Study – Fertilizer Efficiency

Question: *Does MOP give better yields than Urea?*  

```python
df = pd.read_csv("estate_dashboard.csv")

pivot = pd.pivot_table(
    df,
    values="Yield_tonnes",
    index="Block",
    columns="Fertilizer_Type",
    aggfunc="mean"
)
print(pivot)
```

👉 Output shows average yield by fertilizer type per block.  

---

## 15.6 Reflection Questions
1. Why are pivot tables better than looping manually through data?  
2. How can crosstabs help detect fertilizer allocation patterns?  
3. If Block B has higher rainfall but lower yields than Block D, what might that suggest?  

---

## 15.7 Practice Exercises

**Exercise 15.1 – Fertilizer Crosstab**  
- Use `fertilizer.csv`.  
- Build a crosstab showing fertilizer type usage per block.  

**Exercise 15.2 – Yield Pivot**  
- Use `block_yields.csv`.  
- Build a pivot table of average yields by Block and Month.  

**Exercise 15.3 – Rainfall & Yield by Quarter**  
- Use `estate_dashboard.csv`.  
- Build a pivot table showing average rainfall and average yield per block, per quarter.  

**Exercise 15.4 – Soil Type Join**  
- Merge `estate_dashboard.csv` with `estate_info.csv`.  
- Build a pivot table comparing average YPH across soil types.  

**Exercise 15.5 – Challenge**  
- Using `estate_dashboard.csv`:  
  - Build a pivot table comparing **Yield per Hectare** for each fertilizer type across all blocks.  
  - Identify which fertilizer consistently gives the highest YPH.  

---

## 15.8 Section Summary
- **Crosstabs** count categorical combinations.  
- **Pivot tables** summarize metrics across multiple dimensions (block × month, block × fertilizer type).  
- Multi-variable exploration is essential for management insights: fertilizer effectiveness, rainfall impact, soil differences.  

**Take-home Challenge:**  
Using `estate_dashboard.csv`:  
1. Build a pivot table showing quarterly YPH per block.  
2. Build another pivot comparing average productivity (`Tonnes_Harvested / Workers`) across fertilizer types.  
3. Write 3 insights for management.  
