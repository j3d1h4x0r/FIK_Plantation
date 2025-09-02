# Section 9: Python with Pandas – The Data Analyst’s Tool

## 9.1 Why Pandas?
Pandas is a Python library for **data analysis**. It provides two powerful objects:  

- **Series** → like a single column in Excel (1D data).  
- **DataFrame** → like a whole spreadsheet (2D table).  

**Analogy:**  
- A Series is like a single plantation logbook for rainfall.  
- A DataFrame is like the entire office filing cabinet: rainfall, yields, labor, fertilizer—all in one.  

With Pandas, you can load thousands of rows instantly, filter, clean, analyze, and visualize data without tedious manual effort.  

---

## 9.2 Importing Pandas
```python
import pandas as pd
```

By convention, we import Pandas as `pd`.  

---

## 9.3 Reading CSV Files into DataFrames

### Example: Load Rainfall Data
```python
import pandas as pd

df = pd.read_csv("rainfall.csv")
print(df.head())
```

👉 Output:  
```
  Month Block  Rainfall_mm
0   Jan     A          185
1   Feb     A          210
2   Mar     A          198
3   Apr     A          240
4   May     A          260
```  

---

## 9.4 Exploring the DataFrame

### Quick Look
```python
print(df.head())     # first 5 rows
print(df.tail())     # last 5 rows
print(df.shape)      # (rows, columns)
print(df.columns)    # column names
print(df.info())     # data types + memory usage
print(df.describe()) # summary stats (mean, std, min, max)
```

---

## 9.5 Selecting Columns & Rows

### Columns
```python
print(df["Rainfall_mm"])   # one column
print(df[["Month","Rainfall_mm"]])   # multiple columns
```

### Rows with `.iloc` and `.loc`
```python
print(df.iloc[0])   # first row
print(df.loc[0:3])  # rows by index range
```

---

## 9.6 Filtering Data
```python
# Rainfall > 220 mm
wet_months = df[df["Rainfall_mm"] > 220]
print(wet_months)

# Only Block A
block_a = df[df["Block"] == "A"]
print(block_a)
```

---

## 9.7 Sorting Data
```python
sorted_df = df.sort_values("Rainfall_mm", ascending=False)
print(sorted_df.head())
```

---

## 9.8 Grouping & Aggregation

Example: Average rainfall per block.  
```python
avg_rainfall = df.groupby("Block")["Rainfall_mm"].mean()
print(avg_rainfall)
```

Output:  
```
Block
A    209.0
B    222.5
C    190.8
D    235.0
```

---

## 9.9 Plantation Case Study – Estate Dashboard Data

Let’s load **estate_dashboard.csv**.  

```python
df = pd.read_csv("estate_dashboard.csv")
print(df.head())
```

👉 Columns: `Month, Block, Rainfall_mm, Yield_tonnes, Area_ha, Fertilizer_kg, Workers, Tonnes_Harvested, Fertilizer_Type`  

**Examples:**
```python
# Average yield per block
print(df.groupby("Block")["Yield_tonnes"].mean())

# Total fertilizer use by block
print(df.groupby("Block")["Fertilizer_kg"].sum())

# Correlation between rainfall and yield
print(df[["Rainfall_mm","Yield_tonnes"]].corr())
```

---

## 9.10 Reflection Questions
1. How is a Pandas DataFrame different from an Excel sheet?  
2. Why is `.groupby()` powerful for estate data?  
3. How would you analyze whether rainfall impacts yield?  

---

## 9.11 Practice Exercises

**Exercise 9.1 – Basic Exploration**  
- Load `block_yields.csv`.  
- Print first 10 rows, column names, and summary statistics.  

**Exercise 9.2 – Filtering**  
- From `rainfall.csv`, print all months where rainfall < 180 mm in Block C.  

**Exercise 9.3 – Sorting**  
- From `block_yields.csv`, sort yields in descending order.  

**Exercise 9.4 – Aggregation**  
- From `fertilizer.csv`, compute total fertilizer use per block.  

**Exercise 9.5 – Challenge**  
- From `estate_dashboard.csv`:  
  - Compute average Yield per Hectare (Yield_tonnes / Area_ha) by block.  
  - Find which block had the **highest labor productivity** (Tonnes_Harvested / Workers).  

---

## 9.12 Section Summary
- Pandas turns CSV files into powerful DataFrames.  
- You can explore with `.head()`, `.info()`, `.describe()`.  
- Filtering, sorting, and grouping allow **deep insights**.  
- Plantation use cases: rainfall patterns, yield comparisons, fertilizer efficiency, labor productivity.  

**Take-home Challenge:**  
Using `estate_dashboard.csv`:  
1. Calculate average Yield per Hectare for each block.  
2. Find the month with the highest rainfall in Block D.  
3. Compute total tonnes harvested by all blocks combined.  
4. Save the results into a new file `estate_summary.csv`.  
