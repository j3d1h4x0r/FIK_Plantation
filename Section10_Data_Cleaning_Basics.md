# Section 10: Data Cleaning Basics

## 10.1 Why Data Cleaning Matters
In plantation management, data isn’t always perfect. Workers may forget to log rainfall, fertilizer records might be incomplete, or someone may type `"MOP "` (with a space) instead of `"MOP"`.  

Without cleaning, your analysis is misleading. Garbage in → garbage out.  

**Analogy:** If harvesting records are written in smudged ink, the estate manager can’t make correct decisions. Cleaning the data is like re-copying the ledger neatly before reporting.  

---

## 10.2 Common Data Issues in Plantations
1. **Missing values** – e.g., rainfall not recorded for a month.  
2. **Inconsistent labels** – `"MOP"`, `"mop"`, `"M.O.P"`.  
3. **Wrong data types** – `"250"` (string) instead of `250` (integer).  
4. **Outliers** – unrealistic values (rainfall = 2000 mm in a month).  

---

## 10.3 Loading a Dirty Dataset
We’ll use **fertilizer.csv**.  

```python
import pandas as pd

df = pd.read_csv("fertilizer.csv")
print(df.head(15))
```

👉 Notice possible issues: fertilizer type inconsistencies, maybe some missing values if we simulate them later.  

---

## 10.4 Checking for Missing Data
```python
print(df.isnull().sum())   # counts missing values per column
```

👉 If you had missing entries, they’d show up here.  

---

## 10.5 Handling Missing Values

### Drop Missing Values
```python
df_clean = df.dropna()
```

### Fill Missing Values
```python
df["Fertilizer_kg"].fillna(df["Fertilizer_kg"].mean(), inplace=True)
```

👉 Example: If fertilizer log for July is missing, replace with average of other months.  

---

## 10.6 Cleaning Inconsistent Categories
Example: Fertilizer type inconsistencies.  

```python
df["Fertilizer_Type"] = df["Fertilizer_Type"].str.strip().str.upper()
print(df["Fertilizer_Type"].unique())
```

👉 Output: `['MOP', 'UREA', 'NPK']`  

---

## 10.7 Converting Data Types
Sometimes numbers are read as text.  

```python
df["Fertilizer_kg"] = pd.to_numeric(df["Fertilizer_kg"], errors="coerce")
```

---

## 10.8 Detecting Outliers
Example: Rainfall above 1000 mm is likely an error.  

```python
df_outliers = df[df["Fertilizer_kg"] > 500]
print(df_outliers)
```

👉 You can flag these for review instead of deleting immediately.  

---

## 10.9 Plantation Case Study – Estate Dashboard
We’ll use **estate_dashboard.csv**.  

```python
df = pd.read_csv("estate_dashboard.csv")

# Check data types
print(df.dtypes)

# Fix Tonnes_Harvested column if it’s stored as string
df["Tonnes_Harvested"] = pd.to_numeric(df["Tonnes_Harvested"], errors="coerce")

# Normalize Fertilizer_Type column
df["Fertilizer_Type"] = df["Fertilizer_Type"].str.strip().str.upper()
```

👉 Now the data is ready for proper analysis.  

---

## 10.10 Reflection Questions
1. Why should you check for missing values before analysis?  
2. When is it better to drop missing data vs fill it?  
3. Why is standardizing categories (like fertilizer type) important for management decisions?  

---

## 10.11 Practice Exercises

**Exercise 10.1 – Missing Values**  
- Load `fertilizer.csv`.  
- Count missing values.  
- Fill missing `Fertilizer_kg` with the mean value.  

**Exercise 10.2 – Cleaning Categories**  
- Standardize all fertilizer types to uppercase.  
- Count how many times each type was used.  

**Exercise 10.3 – Type Conversion**  
- Load `estate_dashboard.csv`.  
- Ensure `Tonnes_Harvested` is numeric.  

**Exercise 10.4 – Outlier Detection**  
- From `rainfall.csv`, find any months with rainfall > 300 mm.  

**Exercise 10.5 – Challenge**  
- From `estate_dashboard.csv`:  
  - Drop rows with missing values in key columns (`Yield_tonnes`, `Workers`).  
  - Create a cleaned dataset `estate_dashboard_clean.csv`.  

---

## 10.12 Section Summary
- Plantation data often has missing values, inconsistent labels, wrong types, or outliers.  
- Pandas makes cleaning easy: `.isnull()`, `.fillna()`, `.dropna()`.  
- Always standardize categories and check data types.  
- Cleaning is essential before doing any serious analysis.  

**Take-home Challenge:**  
Clean `fertilizer.csv` completely:  
1. Fill missing values.  
2. Standardize fertilizer type.  
3. Detect and report outliers.  
4. Save as `fertilizer_clean.csv`.  
