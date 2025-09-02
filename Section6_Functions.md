# Section 6: Functions – Reusable Code

## 6.1 What Are Functions?
A **function** is a block of code that performs a specific task.  
You can run it whenever needed, instead of writing the same code again and again.

**Plantation Analogy:**  
A function is like a *standard operating procedure (SOP)*. Once you create the SOP for “calculating yield per hectare,” you don’t rewrite it each time—just follow the procedure.

---

## 6.2 Defining a Function
Use the `def` keyword to define a function.

```python
def greet_estate():
    print("Welcome to the plantation system")
```

Call the function:
```python
greet_estate()
```

---

## 6.3 Functions with Parameters
Parameters allow you to pass information into the function.

```python
def greet_manager(name):
    print("Good morning,", name)

greet_manager("Mr. Ali")
greet_manager("Ms. Tan")
```

---

## 6.4 Functions with Return Values
Functions can return results to the caller.

```python
def calculate_yph(tonnes, hectares):
    return tonnes / hectares

result = calculate_yph(250, 50)
print("Yield per hectare:", result)
```

---

## 6.5 Default Parameters
You can give a parameter a default value.

```python
def fertilizer_cost(tonnes, price_per_tonne=1200):
    return tonnes * price_per_tonne

print(fertilizer_cost(10))         # Uses default price
print(fertilizer_cost(10, 1500))   # Uses custom price
```

---

## 6.6 Variable Scope
- **Local variables** exist only inside the function.  
- **Global variables** exist throughout the program.  

Example:
```python
estate_name = "Sungai Tekam"   # global

def show_estate():
    estate_name = "Sabah Estate"  # local
    print("Inside function:", estate_name)

show_estate()
print("Outside function:", estate_name)
```

---

## 6.7 Plantation Use Cases

### Example 1 – Yield per Hectare Function
```python
def calculate_yph(tonnes, hectares):
    return tonnes / hectares

print("Block A YPH:", calculate_yph(25.4, 10.5))
print("Block B YPH:", calculate_yph(31.2, 12.0))
```

### Example 2 – Labor Productivity
```python
def labor_productivity(tonnes, workers):
    return tonnes / workers

print("Productivity:", labor_productivity(120, 30), "tonnes/worker")
```

### Example 3 – Fertilizer Efficiency
```python
def fertilizer_efficiency(yield_increase, fertilizer_kg):
    return yield_increase / fertilizer_kg

print("Efficiency:", fertilizer_efficiency(5.0, 200), "tonnes per kg fertilizer")
```

---

## 6.8 Reflection Questions
1. Why do we use functions instead of repeating code?  
2. What is the difference between a parameter and a return value?  
3. How can functions make plantation data analysis more efficient?  

---

## 6.9 Practice Exercises

**Exercise 6.1 – Simple Function**  
- Write a function `greet_estate(name)` that prints a welcome message with the estate’s name.  

**Exercise 6.2 – Yield Per Hectare**  
- Write a function `calculate_yph(tonnes, hectares)`.  
- Use it to calculate YPH for 3 different blocks.  

**Exercise 6.3 – Cost Per Tonne**  
- Write a function that takes `total_cost` and `tonnes` and returns cost per tonne.  

**Exercise 6.4 – Rainfall Classification**  
- Write a function that takes rainfall (mm) and returns:  
  - “Dry” if <200,  
  - “Normal” if 200–250,  
  - “Wet” if >250.  

**Exercise 6.5 – Challenge**  
- Create a dictionary with block yields and hectares.  
- Write a function that loops through the dictionary and prints YPH for each block.  

---

## 6.10 Section Summary
- Functions are reusable blocks of code.  
- Parameters allow you to pass values into functions.  
- Return values give results back.  
- Default parameters make functions flexible.  
- Plantation use cases: YPH, labor productivity, fertilizer efficiency.  

**Take-home Challenge:**  
Write a program with three functions:  
1. `calculate_yph(tonnes, hectares)`  
2. `labor_productivity(tonnes, workers)`  
3. `cost_per_tonne(cost, tonnes)`  

Ask the user for input values and print a complete estate performance summary.  
