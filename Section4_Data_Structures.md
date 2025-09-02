# Section 4: Data Structures – Lists, Tuples, and Dictionaries

## 4.1 What Are Data Structures?
A data structure is a way of organizing and storing data so it can be used efficiently.  
Python provides several built-in data structures. The most commonly used in beginner projects are:

- **Lists**: Ordered, changeable collections.
- **Tuples**: Ordered, unchangeable collections.
- **Dictionaries**: Unordered collections of key-value pairs.

**Plantation Analogy:**  
- A list is like a logbook of daily yields, where you can add new entries or correct mistakes.  
- A tuple is like a recorded agreement—you can read it but not change it.  
- A dictionary is like a store room where each item has a label and content (key-value).  

---

## 4.2 Lists
Lists are used to store multiple items in a single variable. They are ordered and changeable.

### Creating Lists
```python
rainfall_q1 = [210.5, 185.2, 230.1]
yields = [25.4, 31.2, 28.9]
```

### Accessing List Items
```python
print(rainfall_q1[0])   # First item
print(yields[-1])       # Last item
```

### Modifying Lists
```python
yields[0] = 26.0   # Update Block A’s yield
print(yields)
```

### Useful List Functions
```python
print(len(yields))      # Length of list
print(sum(yields))      # Total yield
print(min(yields))      # Minimum yield
print(max(yields))      # Maximum yield
```

---

## 4.3 Tuples
Tuples are like lists, but once created, they cannot be changed (immutable).

```python
estate_info = ("Sungai Tekam", "Pahang", 4500)
print(estate_info[0])   # Estate name
```

**When to use tuples:**  
- When you want to store data that should not change, e.g., estate coordinates (latitude, longitude).

```python
estate_coordinates = (3.735, 102.512)
```

---

## 4.4 Dictionaries
Dictionaries store data in key-value pairs.

### Creating a Dictionary
```python
block_yields = {
    "Block A": 25.4,
    "Block B": 31.2,
    "Block C": 28.9
}
```

### Accessing Values
```python
print(block_yields["Block A"])   # 25.4
```

### Adding or Updating Items
```python
block_yields["Block D"] = 30.5
block_yields["Block A"] = 26.0
```

### Removing Items
```python
del block_yields["Block C"]
```

### Looping Through a Dictionary
```python
for block, yield_val in block_yields.items():
    print(block, ":", yield_val)
```

---

## 4.5 Plantation Use Cases

### Example 1 – Rainfall Analysis
```python
rainfall_monthly = [180, 220, 200, 190, 250]
average_rainfall = sum(rainfall_monthly) / len(rainfall_monthly)
print("Average Rainfall:", average_rainfall)
```

### Example 2 – Block Yield Dictionary
```python
block_yields = {
    "Block A": 25.4,
    "Block B": 31.2,
    "Block C": 28.9
}
for block, yph in block_yields.items():
    print(block, "yield is", yph, "tonnes")
```

### Example 3 – Estate Info (Tuple)
```python
estate_info = ("FGV Plantation", "Johor", 3000)
print("Estate Name:", estate_info[0])
print("Location:", estate_info[1])
print("Size (ha):", estate_info[2])
```

---

## 4.6 Reflection Questions
1. How is a list different from a tuple?  
2. Why would you use a dictionary instead of a list?  
3. Give a plantation example where a tuple is more suitable than a list.  

---

## 4.7 Practice Exercises

**Exercise 4.1 – Lists**  
- Create a list of yields from 4 blocks.  
- Print the total and average yield.  
- Update Block 2’s yield.  

**Exercise 4.2 – Tuples**  
- Create a tuple with estate name, state, and total area.  
- Print each value.  

**Exercise 4.3 – Dictionaries**  
- Create a dictionary with rainfall values for Jan, Feb, and Mar.  
- Add April’s rainfall.  
- Update February’s rainfall.  
- Loop through and print all months with rainfall.  

**Exercise 4.4 – Mixed Challenge**  
- Create a dictionary where each key is a block, and the value is a tuple (yield, hectares).  
- Loop through the dictionary and calculate yield per hectare for each block.  

---

## 4.8 Section Summary
- **Lists** are ordered, changeable collections.  
- **Tuples** are ordered but unchangeable.  
- **Dictionaries** store key-value pairs.  
- Each has practical plantation use cases (rainfall tracking, block yields, estate info).  

**Take-home Challenge:** Build a dictionary for your estate with:  
- Estate name, location, size (ha), total workers.  
- Nested dictionary: block names as keys, each storing a list of monthly yields.  
- Print a detailed estate summary report.  
