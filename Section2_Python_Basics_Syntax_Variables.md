# Section 2: Python Basics – Syntax & Variables

## 2.1 Python Syntax Rules
Python has a unique style compared to other programming languages. The most important rule is **indentation**.

### Indentation
Indentation means spaces at the beginning of a line. Python uses indentation to group code blocks instead of curly braces `{}`.

Example:
```python
if 10 > 5:
    print("10 is greater than 5")
```

If you remove the spaces:
```python
if 10 > 5:
print("10 is greater than 5")   # This will cause an IndentationError
```

**Plantation Analogy:** Indentation is like planting oil palms in straight lines. Without alignment, the estate looks messy and becomes unmanageable.

---

## 2.2 Case Sensitivity
Python is case-sensitive.  
- `Yield` and `yield` are two different variables.

Example:
```python
Yield = 100
yield = 80
print(Yield)  # 100
print(yield)  # 80
```

---

## 2.3 Comments
Comments are ignored by Python but help explain your code.

```python
# This is a comment
print("Harvesting started")  # This is also a comment
```

**Multi-line comments:**
```python
"""
This program calculates
the yield per hectare.
"""
```

---

## 2.4 Variables
A variable is like a labeled container that stores information.

### Rules for Variable Names:
- Must start with a letter or underscore.
- Cannot start with a number.
- No spaces (use underscores instead).
- Case-sensitive.

Examples:
```python
estate_name = "Sungai Tekam"
block_a_yield = 25.4
number_of_workers = 15
```

---

## 2.5 Data Types
Python has different types of data.

- **Integer (int)**: Whole numbers → `45` harvesters.  
- **Float (float)**: Decimal numbers → `25.4` tonnes.  
- **String (str)**: Text inside quotes → `"Sungai Tekam"`.  
- **Boolean (bool)**: True/False values.

```python
harvesters = 45          # int
rainfall_today = 18.5    # float
estate = "FGV Plantation" # string
fertilizer_ready = True   # boolean
```

---

## 2.6 Type Conversion (Casting)
Change one type into another.

```python
rainfall_str = "25.5"
rainfall_float = float(rainfall_str)
print(rainfall_float + 10)   # 35.5
```

---

## 2.7 The input() Function
The `input()` function lets you interact with the user.

```python
estate_name = input("Enter estate name: ")
print("Welcome to", estate_name)
```

**Exercise 2.1:** Write a program that asks the user for today’s rainfall and prints it.

---

## 2.8 Plantation Example
```python
estate_name = "Sungai Tekam"
block_a_yield = 25.4
block_b_yield = 31.2
total_yield = block_a_yield + block_b_yield

print("Estate:", estate_name)
print("Block A Yield:", block_a_yield, "tonnes")
print("Block B Yield:", block_b_yield, "tonnes")
print("Total Yield:", total_yield, "tonnes")
```

Output:
```
Estate: Sungai Tekam
Block A Yield: 25.4 tonnes
Block B Yield: 31.2 tonnes
Total Yield: 56.6 tonnes
```

---

## 2.9 Reflection Questions
1. Why is indentation important in Python?
2. What’s the difference between an integer and a float?
3. Why is case sensitivity useful in programming?

---

## 2.10 Practice Exercises

**Exercise 2.2 – Variables Practice**  
- Create variables for estate name, manager name, and number of harvesters.  
- Print a welcome message that includes all three.  

**Exercise 2.3 – Data Types**  
- Create one variable of each type: int, float, string, boolean.  
- Print them with labels.  

**Exercise 2.4 – Type Conversion**  
- Store rainfall as a string `"20.5"`.  
- Convert it into a float and add 5.  

**Exercise 2.5 – User Input**  
- Ask the user for estate name and rainfall.  
- Print a short report using these values.  

---

## 2.11 Section Summary
- Python relies on indentation for structure.  
- Variables are containers that store values.  
- Python has different data types (int, float, str, bool).  
- You can convert between types when needed.  
- `input()` lets users interact with the program.  

**Take-home Challenge:** Write a Python script that:  
1. Asks the user for estate name, number of blocks, and rainfall today.  
2. Prints a formatted report showing this data.  
