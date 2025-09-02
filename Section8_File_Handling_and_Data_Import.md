# Section 8: File Handling & Data Import

## 8.1 Why File Handling Matters in Plantations
In the real world, estate data does not live in neat variables inside your Python program. Instead, it lives in **files**: spreadsheets, rainfall logs, harvest reports, labor sheets, and fertilizer usage reports.  

- **Without Python:** You open Excel manually, copy-paste, and compute.  
- **With Python:** You read 12 files in seconds, combine them, and summarize automatically.  

**Analogy:** File handling is like accessing estate logbooks from storage. Instead of flipping through dusty ledgers, Python acts as your clerk—fetching, reading, and summarizing entries instantly.  

---

## 8.2 Reading and Writing Text Files

### Open and Read Files
```python
# Opening a file (mode = 'r' for read)
f = open("rainfall.txt", "r")
print(f.read())
f.close()
```

### Writing to Files
```python
# Writing to a text file
f = open("notes.txt", "w")
f.write("Block A harvested 25 tonnes today.")
f.close()
```

### Best Practice: Use `with`
```python
with open("notes.txt", "w") as f:
    f.write("Block B harvested 30 tonnes today.")
```

**Exercise 8.1:**  
- Create a text file called `harvest_log.txt`.  
- Write “Today’s rainfall: 220mm” into it.  
- Reopen it and print the content.  

---

## 8.3 Working with CSV Files
CSV (Comma-Separated Values) files are the most common format for plantation data (e.g., rainfall logs, yield records).  

### Reading CSV with Python’s `csv` module
```python
import csv

with open("rainfall.csv", "r") as f:
    reader = csv.reader(f)
    for row in reader:
        print(row)
```

Output:
```
['Month', 'Block', 'Rainfall_mm']
['Jan', 'A', '185']
['Feb', 'A', '210']
...
```

### Writing to CSV
```python
import csv

data = [
    ["Month", "Block", "Rainfall_mm"],
    ["Jan", "A", 185],
    ["Feb", "A", 210]
]

with open("rainfall_new.csv", "w", newline="") as f:
    writer = csv.writer(f)
    writer.writerows(data)
```

---

## 8.4 Practical Example: Plantation Rainfall Logs
We’ll use **rainfall.csv** (already provided).  

```python
import csv

with open("rainfall.csv", "r") as f:
    reader = csv.DictReader(f)
    total = 0
    count = 0
    for row in reader:
        if row["Block"] == "A":
            total += float(row["Rainfall_mm"])
            count += 1

print("Average Rainfall for Block A:", total/count)
```

👉 Output: `Average Rainfall for Block A: 209.0 mm`  

---

## 8.5 Error Handling in File Operations
Sometimes files are missing or corrupted. Python allows you to handle these gracefully.  

```python
try:
    with open("nonexistent.csv", "r") as f:
        print(f.read())
except FileNotFoundError:
    print("File not found. Please check the filename.")
```

---

## 8.6 Plantation Case Study: Yield Summary from File
We’ll use **block_yields.csv**.  

```python
import csv

with open("block_yields.csv", "r") as f:
    reader = csv.DictReader(f)
    total_yield = 0
    for row in reader:
        total_yield += float(row["Yield_tonnes"])

print("Total Estate Yield:", total_yield, "tonnes")
```

---

## 8.7 Reflection Questions
1. Why do estates often use CSV files instead of Excel files for data transfer?  
2. How does using `with open()` improve your file-handling scripts?  
3. What kind of plantation data would you keep in text vs CSV formats?  

---

## 8.8 Practice Exercises

**Exercise 8.2 – Rainfall Average**  
- Read `rainfall.csv`.  
- Calculate average rainfall for Block B.  

**Exercise 8.3 – High Rainfall Months**  
- Read `rainfall.csv`.  
- Print all months where rainfall > 240 mm for Block D.  

**Exercise 8.4 – Writing Harvest Notes**  
- Create a file `daily_report.txt`.  
- Write: *“Estate Sungai Tekam harvested 250 tonnes today with 120 workers.”*  
- Reopen it and print the contents.  

**Exercise 8.5 – Challenge**  
- Read `block_yields.csv`.  
- Compute Yield per Hectare for each block and write the results to a new file `yph_report.csv`.  

---

## 8.9 Section Summary
- Python can **read/write text files** easily.  
- CSV files are essential for plantation data exchange.  
- With Python, you can **analyze CSVs directly** instead of doing manual Excel work.  
- Error handling ensures your program doesn’t crash if files are missing.  

**Take-home Challenge:**  
Create a script that:  
1. Reads rainfall from `rainfall.csv`.  
2. Computes the average rainfall for each block.  
3. Writes results to `rainfall_summary.csv`.  
