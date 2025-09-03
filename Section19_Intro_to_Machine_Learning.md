# Section 19: Intro to Machine Learning (Scikit-learn Primer)

## 19.1 Why Machine Learning in Plantations?
So far, we’ve explored, cleaned, and visualized data. But managers often ask:  

- *“Can you predict next month’s yield?”*  
- *“How much fertilizer should we apply to reach target production?”*  
- *“Which factor matters more: rainfall, workers, or fertilizer?”*  

This is where **machine learning (ML)** helps. It uses historical data to build **models** that can predict outcomes and highlight key drivers.  

**Analogy:** If statistics is like looking at a photo album, ML is like teaching a friend to predict what tomorrow’s photo will look like based on past ones.  

---

## 19.2 Core Concepts
- **Features (X):** Inputs (rainfall, fertilizer, workers).  
- **Target (y):** Output we want to predict (yield).  
- **Model:** A mathematical formula that learns from data.  
- **Train/Test Split:** Train the model on some data, test accuracy on the rest.  

---

## 19.3 First Model – Linear Regression

### Predicting Yield from Rainfall & Fertilizer
```python
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error, r2_score

# Load data
df = pd.read_csv("estate_dashboard.csv")

# Features (inputs)
X = df[["Rainfall_mm","Fertilizer_kg","Workers"]]

# Target (output)
y = df["Yield_tonnes"]

# Split data into training and test sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Build model
model = LinearRegression()
model.fit(X_train, y_train)

# Predictions
y_pred = model.predict(X_test)

# Evaluation
print("Coefficients:", model.coef_)
print("Intercept:", model.intercept_)
print("R² Score:", r2_score(y_test, y_pred))
print("MSE:", mean_squared_error(y_test, y_pred))
```
👉 R² shows how well features explain yield (closer to 1 = better).  

---

## 19.4 Understanding Coefficients
Example output:  
```
Rainfall_mm   0.08
Fertilizer_kg 0.12
Workers       0.30
```

Interpretation:  
- Each extra mm of rainfall adds **0.08 tonnes** (on average).  
- Each kg of fertilizer adds **0.12 tonnes**.  
- Each worker adds **0.30 tonnes**.  

---

## 19.5 Case Study – Predicting Block Yields
```python
new_data = pd.DataFrame({
    "Rainfall_mm": [250, 180],
    "Fertilizer_kg": [400, 300],
    "Workers": [25, 20]
})

predictions = model.predict(new_data)
print(predictions)
```
👉 Model predicts expected yield for given inputs.  

---

## 19.6 Beyond Linear Regression
- **Decision Trees:** Split data into rules (if rainfall > 200, yield ↑).  
- **Random Forests:** Multiple trees for robust predictions.  
- **Logistic Regression:** Classify outcomes (e.g., “High Yield” vs “Low Yield”).  

We start with **linear regression** because it’s simple and explainable for management.  

---

## 19.7 Reflection Questions
1. Why do we split data into training and test sets?  
2. How would you explain coefficients to a non-technical estate manager?  
3. What risks come with using ML predictions in plantation planning?  

---

## 19.8 Practice Exercises

**Exercise 19.1 – Simple Regression**  
- Use `estate_dashboard.csv`.  
- Predict yield using **Rainfall only**.  

**Exercise 19.2 – Multi-Feature Regression**  
- Add Fertilizer and Workers as predictors.  
- Compare R² scores with the single-variable model.  

**Exercise 19.3 – Predictions**  
- Predict yield for: Rainfall=220, Fertilizer=350, Workers=28.  

**Exercise 19.4 – Challenge**  
- Train a model with Rainfall, Fertilizer, Workers, and Area.  
- Identify which factor contributes most strongly to yield (largest coefficient).  

---

## 19.9 Section Summary
- ML predicts outcomes by learning patterns from data.  
- Features → input variables; Target → output variable.  
- Linear regression is a simple but powerful model for yield prediction.  
- Models help guide decisions but must be tested for accuracy.  

**Take-home Challenge:**  
Using `estate_dashboard.csv`:  
1. Build a regression model predicting yield from Rainfall, Fertilizer, and Workers.  
2. Compare actual vs predicted yields on test data.  
3. Write 3 insights for management:  
   - Which factor most impacts yield?  
   - How accurate is the model?  
   - How could this guide fertilizer/labor allocation next season?  
