# Section 11: Data Exploration & Summary Statistics

## 11.1 Why Explore Data?
Before you run complex models or generate fancy charts, you must **understand your data**.  

- Is rainfall normally distributed or skewed?  
- Does fertilizer use really correlate with yield?  
- Are there big differences between blocks?  

Exploration = looking for **patterns, anomalies, and relationships**.  

**Analogy:** Before cooking, a chef tastes ingredients separately. Data exploration is the tasting stage—you check quality before mixing.  

---

## 11.2 Key Statistical Measures

### Mean (Average)
```python
import pandas as pd

df = pd.read_csv("block_yields.csv")
print(df["Yield_tonnes"].mean())
```

### Median
```python
print(df["Yield_tonnes"].median())
```

### Mode
```python
print(df["Yield_tonnes"].mode())
```

---

### Variance & Standard Deviation
Variance shows spread, standard deviation (SD) shows average deviation.  

```python
print(df["Yield_tonnes"].var())
print(df["Yield_tonnes"].std())
```

---

### Correlation
Correlation measures how strongly two variables move together.  

```python
df = pd.read_csv("estate_dashboard.csv")
print(df[["Rainfall_mm","Yield_tonnes"]].corr())
```

👉 If correlation is **positive**, more rain → more yield.  
👉 If **negative**, more rain → lower yield (possible flooding).  

---

## 11.3 Exploring Rainfall and Yield
```python
df = pd.read_csv("estate_dashboard.csv")

avg_rainfall = df["Rainfall_mm"].mean()
avg_yield = df["Yield_tonnes"].mean()

print("Average Rainfall:", avg_rainfall)
print("Average Yield:", avg_yield)

# Correlation
print(df[["Rainfall_mm","Yield_tonnes"]].corr())
```

---

## 11.4 Grouping and Aggregating

Example: Average yield per block.  

```python
print(df.groupby("Block")["Yield_tonnes"].mean())
```

👉 Output:
```
Block
A    25.9
B    30.4
C    23.2
D    33.0
```

---

## 11.5 Plantation Case Study – Fertilizer vs Yield

Is fertilizer effective?  

```python
print(df[["Fertilizer_kg","Yield_tonnes"]].corr())
```

👉 If correlation is weak or negative → maybe fertilizer timing or application method is wrong.  

---

## 11.6 Detecting Skewness & Distribution

### Histogram with Pandas
```python
df["Yield_tonnes"].hist()
```

### Skewness & Kurtosis
```python
print(df["Yield_tonnes"].skew())    # symmetry
print(df["Yield_tonnes"].kurt())    # peakedness
```

---

## 11.7 Reflection Questions
1. What does a **high standard deviation** mean for estate yields?  
2. Why is correlation not the same as causation?  
3. How could skewness in rainfall distribution affect plantation planning?  

---

## 11.8 Practice Exercises

**Exercise 11.1 – Mean & Median**  
- From `rainfall.csv`, compute mean and median rainfall for Block C.  

**Exercise 11.2 – Standard Deviation**  
- From `block_yields.csv`, calculate standard deviation of yields for Block A.  

**Exercise 11.3 – Correlation**  
- From `estate_dashboard.csv`, check correlation between Workers and Tonnes_Harvested.  

**Exercise 11.4 – Aggregation**  
- Compute average Yield per Hectare (Yield_tonnes / Area_ha) per block.  

**Exercise 11.5 – Challenge**  
- Identify which block has the **most stable yield** (lowest standard deviation).  
- Identify which block is **most affected by rainfall** (highest correlation with rainfall).  

---

## 11.9 Section Summary
- Mean, median, and mode describe central tendency.  
- Variance and standard deviation show spread.  
- Correlation reveals relationships (but not causation).  
- Skewness and kurtosis describe distribution shapes.  
- Plantation managers can use these stats to understand rainfall-yield patterns, fertilizer efficiency, and block stability.  

**Take-home Challenge:**  
Using `estate_dashboard.csv`:  
1. Find the block with the highest average yield.  
2. Find the block with the highest standard deviation in rainfall.  
3. Which block has the strongest positive correlation between rainfall and yield?  
