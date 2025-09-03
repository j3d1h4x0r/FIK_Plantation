# Section 17: Combining Multiple Data Sources

## 17.1 Why Combine Data?
Each plantation dataset tells only part of the story:  
- **Rainfall.csv** → Weather patterns.  
- **Fertilizer.csv** → Inputs applied.  
- **Block_yields.csv** → Outputs (tonnes harvested).  
- **Labor.csv** → Human effort.  

By combining them, you can uncover relationships:  
- Does high rainfall + high fertilizer = higher yields?  
- Which block achieves the best yield with fewer workers?  

**Analogy:** Think of each dataset as one witness to an event. Only when all witnesses speak together do you get the full story.  

---

## 17.2 Merging Datasets in Pandas

### Example: Merge Fertilizer and Yields
```python
import pandas as pd

fert = pd.read_csv("fertilizer.csv")
yields = pd.read_csv("block_yields.csv")

merged = pd.merge(yields, fert, on=["Month","Block"], how="inner")
print(merged.head())
```
👉 Now you can analyze fertilizer impact on yields month-by-month.  

---

## 17.3 Joining Rainfall and Labor Data
```python
rain = pd.read_csv("rainfall.csv")
labor = pd.read_csv("labor.csv")

combined = pd.merge(rain, labor, on=["Month","Block"], how="inner")
print(combined.head())
```
👉 This lets you check: did high rainfall months require more or fewer workers?  

---

## 17.4 Multi-Dataset Integration – Estate Dashboard
Instead of merging step by step, you can **chain merges** to build one master dataset.  

```python
df = pd.read_csv("block_yields.csv")
rain = pd.read_csv("rainfall.csv")
fert = pd.read_csv("fertilizer.csv")
labor = pd.read_csv("labor.csv")

combined = (
    df.merge(rain, on=["Month","Block"])
      .merge(fert, on=["Month","Block"])
      .merge(labor, on=["Month","Block"])
)

print(combined.head())
```

---

## 17.5 Plantation Case Study – Fertilizer + Rainfall Impact on Yield
```python
case = combined.groupby("Block").agg({
    "Rainfall_mm":"mean",
    "Fertilizer_kg":"mean",
    "Yield_tonnes":"mean"
})
print(case)
```
👉 Managers can see whether higher inputs (rainfall + fertilizer) truly correlate with higher yields.  

---

## 17.6 Reflection Questions
1. Why does combining datasets give richer insights than analyzing them separately?  
2. How do `inner`, `left`, and `outer` joins change the results?  
3. What risks appear when combining datasets (e.g., mismatched months)?  

---

## 17.7 Practice Exercises

**Exercise 17.1 – Merge Basics**  
- Merge `fertilizer.csv` with `block_yields.csv`.  
- Compute correlation between Fertilizer_kg and Yield_tonnes.  

**Exercise 17.2 – Rainfall & Labor**  
- Merge `rainfall.csv` and `labor.csv`.  
- Check if higher rainfall months needed more or fewer workers.  

**Exercise 17.3 – Multi-Merge**  
- Merge rainfall, fertilizer, yield, and labor datasets.  
- Create a new column: **Yield per Worker** = `Yield_tonnes / Workers`.  

**Exercise 17.4 – Soil Data Integration**  
- Merge `estate_info.csv` into the combined dataset.  
- Compare average Yield per Hectare by Soil_Type.  

**Exercise 17.5 – Challenge**  
- Build a master dataset with **all five CSVs**.  
- Answer: Which block delivers the **highest yield per hectare** with the **least fertilizer per tonne**?  

---

## 17.8 Section Summary
- Pandas `merge()` combines multiple datasets on shared keys (e.g., Month, Block).  
- Chaining merges creates a **master view** of plantation performance.  
- Integrated analysis reveals hidden relationships: rainfall × fertilizer × labor × yield.  

**Take-home Challenge:**  
Create `estate_master.csv` by merging rainfall, fertilizer, yields, labor, and soil info. From it, calculate:  
1. Average yield per block.  
2. Yield per worker.  
3. Fertilizer efficiency (yield per kg fertilizer).  
4. Write 3 insights for management.  
