# Section 3: Operators & Expressions

## 3.1 What Are Operators?
Operators are special symbols that tell Python to perform a specific action.  
For example, `+` means addition, `-` means subtraction, and `*` means multiplication.

**Plantation Analogy:** Think of operators like farming tools. Each tool has its job:
- A sickle cuts bunches (like the `-` operator subtracts values).
- A weighing scale adds up bunches (like the `+` operator).
- A fertilizer spreader distributes evenly (like `/` division).

---

## 3.2 Arithmetic Operators
These operators are used for basic mathematical calculations.

| Operator | Meaning | Example | Result |
|----------|---------|---------|--------|
| + | Addition | 10 + 5 | 15 |
| - | Subtraction | 10 - 5 | 5 |
| * | Multiplication | 10 * 5 | 50 |
| / | Division | 10 / 5 | 2.0 |
| % | Modulus (remainder) | 10 % 3 | 1 |
| // | Floor division | 10 // 3 | 3 |
| ** | Exponentiation | 2 ** 3 | 8 |

Example:
```python
tonnes = 120
hectares = 40
yph = tonnes / hectares  # yield per hectare
print("Yield per hectare:", yph)
```

---

## 3.3 Comparison Operators
Comparison operators are used to compare values. They return **True** or **False**.

| Operator | Meaning | Example | Result |
|----------|---------|---------|--------|
| == | Equal | 5 == 5 | True |
| != | Not equal | 5 != 3 | True |
| > | Greater than | 7 > 3 | True |
| < | Less than | 3 < 7 | True |
| >= | Greater or equal | 5 >= 5 | True |
| <= | Less or equal | 4 <= 6 | True |

Example:
```python
yield_tonnes = 30
target = 25
print(yield_tonnes > target)  # True
```

---

## 3.4 Logical Operators
Logical operators combine multiple conditions.

| Operator | Meaning | Example | Result |
|----------|---------|---------|--------|
| and | True if both are true | 5 > 2 and 10 > 5 | True |
| or | True if at least one is true | 5 > 10 or 7 > 3 | True |
| not | Reverses condition | not(5 > 2) | False |

Example:
```python
rainfall = 180
fertilizer_applied = True

if rainfall > 200 and fertilizer_applied:
    print("Expect good yield")
else:
    print("Monitor closely")
```

---

## 3.5 Operator Precedence
Python follows a specific order of operations, just like in mathematics.  
**BODMAS Rule:** Brackets → Orders → Division/Multiplication → Addition/Subtraction.

Example:
```python
result = 10 + 5 * 2
print(result)  # 20, not 30 (multiplication before addition)
```

To change order, use parentheses:
```python
result = (10 + 5) * 2
print(result)  # 30
```

---

## 3.6 Plantation Examples

### Yield per hectare calculation
```python
tonnes = 250
hectares = 50
yph = tonnes / hectares
print("Yield per hectare:", yph)
```

### Cost per tonne calculation
```python
total_cost = 15000
yield_tonnes = 120
cost_per_tonne = total_cost / yield_tonnes
print("Cost per tonne:", cost_per_tonne)
```

### Productivity formula
```python
tonnes = 100
workers = 25
productivity = tonnes / workers
print("Productivity per worker:", productivity, "tonnes")
```

---

## 3.7 Reflection Questions
1. What is the difference between `/` and `//`?  
2. Why do comparison operators return True/False instead of numbers?  
3. How would you calculate fertilizer efficiency using operators?  

---

## 3.8 Practice Exercises

**Exercise 3.1 – Arithmetic**  
- Estate produced 480 tonnes of FFB from 120 hectares. Calculate yield per hectare.  

**Exercise 3.2 – Comparison**  
- Check if yield per hectare is greater than 20.  

**Exercise 3.3 – Logical**  
- If rainfall > 200mm and fertilizer applied is True → print “High yield expected”, else print “Low yield expected”.  

**Exercise 3.4 – Precedence**  
- Calculate `(total_yield + extra_yield) / workers`.  
- Try without brackets and see the difference.  

**Exercise 3.5 – Cost Efficiency**  
- Harvesting cost = RM 20,000. Yield = 200 tonnes.  
- Calculate cost per tonne.  
- Check if cost per tonne is less than RM 100.  

---

## 3.9 Section Summary
- Arithmetic operators help with yield, cost, and productivity calculations.  
- Comparison operators return True/False for decisions.  
- Logical operators combine conditions (rainfall, fertilizer, yield).  
- Precedence matters: always use brackets for clarity.  

**Take-home Challenge:** Write a Python program that:  
1. Stores estate yield, hectares, workers, and cost.  
2. Calculates yield per hectare, productivity, and cost per tonne.  
3. Checks if productivity is above 5 tonnes per worker AND cost per tonne is below RM 100.  
4. Prints “Efficient operation” if true, else “Needs improvement”.  
