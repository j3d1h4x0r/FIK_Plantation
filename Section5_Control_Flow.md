# Section 5: Control Flow – If/Else and Loops

## 5.1 What Is Control Flow?
Control flow determines **how a program makes decisions and repeats actions**.  
- **If/Else statements**: Make choices.  
- **Loops**: Repeat tasks automatically.  

**Plantation Analogy:**  
- If/Else is like a manager deciding: *“If it rains, stop harvesting; else, continue.”*  
- A loop is like telling a worker: *“Check every block’s fertilizer bag for expiry.”*  

---

## 5.2 If Statements
The simplest way to make a decision.

```python
yield_tonnes = 28
if yield_tonnes > 25:
    print("Good harvest")
```

---

## 5.3 If/Else Statements
```python
rainfall = 180
if rainfall >= 200:
    print("Sufficient rainfall")
else:
    print("Irrigation required")
```

---

## 5.4 Elif (Else If)
Use `elif` to check multiple conditions.

```python
rainfall = 150
if rainfall > 250:
    print("Excess rainfall – monitor flooding risk")
elif rainfall >= 200:
    print("Sufficient rainfall")
elif rainfall >= 150:
    print("Moderate rainfall – monitor closely")
else:
    print("Irrigation required")
```

---

## 5.5 Nested If Statements
```python
yield_tonnes = 30
rainfall = 210

if yield_tonnes > 25:
    if rainfall > 200:
        print("High yield supported by rainfall")
```

---

## 5.6 For Loops
For loops let you repeat a task for each item in a list.

```python
block_yields = [25.4, 31.2, 28.9]

for yield_val in block_yields:
    print("Block yield:", yield_val)
```

---

## 5.7 While Loops
A while loop repeats as long as a condition is True.

```python
workers = 5
while workers > 0:
    print("Worker available:", workers)
    workers -= 1
```

⚠️ Be careful: If you forget to reduce the counter, it becomes an **infinite loop**.  

---

## 5.8 Loop with Range()
```python
for day in range(1, 6):
    print("Harvesting Day", day)
```

---

## 5.9 Plantation Examples

### Example 1 – Classifying Yields
```python
block_yields = [25.4, 18.2, 31.0, 12.5]

for yield_val in block_yields:
    if yield_val >= 25:
        print("High yield:", yield_val)
    else:
        print("Low yield:", yield_val)
```

### Example 2 – Monthly Rainfall
```python
rainfall_months = [180, 220, 200, 190, 250]

for rainfall in rainfall_months:
    if rainfall < 200:
        print(rainfall, "-> Dry month")
    else:
        print(rainfall, "-> Wet month")
```

### Example 3 – Worker Productivity
```python
workers = 10
tonnes = 50

productivity = tonnes / workers

if productivity >= 5:
    print("Good productivity")
else:
    print("Needs improvement")
```

---

## 5.10 Reflection Questions
1. When would you use `elif` instead of multiple `if` statements?  
2. What could happen if you forget to reduce a counter in a while loop?  
3. How can loops save time in processing estate data?  

---

## 5.11 Practice Exercises

**Exercise 5.1 – If/Else**  
- Write a program that checks if rainfall is above 200mm. If yes → print “Good rainfall”, else → print “Irrigation needed”.  

**Exercise 5.2 – Elif**  
- Classify rainfall as:  
  - Above 250 → “Excessive”  
  - 200–250 → “Sufficient”  
  - 150–199 → “Moderate”  
  - Below 150 → “Insufficient”  

**Exercise 5.3 – For Loop**  
- Create a list of yields for 5 blocks.  
- Loop through the list and print whether each block’s yield is “Good” or “Poor” (threshold = 20).  

**Exercise 5.4 – While Loop**  
- Start with 10 workers.  
- Use a while loop to count down workers until 0.  

**Exercise 5.5 – Range Loop**  
- Print days 1 to 7 to simulate a harvesting week.  

**Exercise 5.6 – Challenge**  
- Store monthly rainfall in a list (12 values).  
- Loop through the list and count how many months are “Dry” (<200mm).  

---

## 5.12 Section Summary
- **If/Else** controls decision-making.  
- **Elif** helps check multiple conditions.  
- **For loops** repeat tasks for each item in a list.  
- **While loops** repeat until a condition is False.  
- Loops + conditionals = powerful automation for estate data.  

**Take-home Challenge:**  
Write a program that:  
1. Stores rainfall data for 12 months.  
2. Classifies each month as Dry (<200), Normal (200–250), or Wet (>250).  
3. Prints a summary: number of Dry months, Normal months, and Wet months.  
