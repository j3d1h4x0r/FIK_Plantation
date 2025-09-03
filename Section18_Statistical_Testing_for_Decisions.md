# Section 18: Statistical Testing for Decisions

## 18.1 Why Statistical Testing?
Managers often ask: *“Does MOP fertilizer really give better yields than Urea?”* or *“Did adding 10 extra workers actually increase productivity?”*  

Instead of relying on **gut feeling**, we use **statistical testing** to confirm whether observed differences are **real or just random chance**.  

**Analogy:** If you flip a coin 10 times and get 7 heads, does that mean the coin is biased? Or was it just luck? Statistical tests help answer that.  

---

## 18.2 The Basics of Hypothesis Testing
- **Null Hypothesis (H₀):** No difference. Example: “MOP and Urea give the same yield.”  
- **Alternative Hypothesis (H₁):** There is a difference. Example: “MOP gives higher yield than Urea.”  
- **p-value:** Probability of observing your results (or more extreme) if H₀ is true.  
  - If **p < 0.05** → reject H₀ (statistically significant).  
  - If **p ≥ 0.05** → fail to reject H₀ (could be random).  

---

## 18.3 Example – Fertilizer Comparison (t-test)
```python
import pandas as pd
from scipy import stats

df = pd.read_csv("estate_dashboard.csv")

mop = df[df["Fertilizer_Type"]=="MOP"]["Yield_tonnes"]
urea = df[df["Fertilizer_Type"]=="UREA"]["Yield_tonnes"]

t_stat, p_val = stats.ttest_ind(mop, urea, equal_var=False)
print("t-stat:", t_stat, "p-value:", p_val)
```
👉 If `p < 0.05`, we conclude MOP yields are significantly different from Urea yields.  

---

## 18.4 Example – Labor Impact (Paired Test)
Suppose Block A used 20 workers in Jan and 30 workers in Feb. Did yield change significantly?  

```python
before = [22.5, 24.0, 23.1]  # yields before extra workers
after = [25.4, 26.1, 25.9]   # yields after extra workers

t_stat, p_val = stats.ttest_rel(before, after)
print("t-stat:", t_stat, "p-value:", p_val)
```
👉 A paired t-test compares before-and-after values for the **same block**.  

---

## 18.5 Chi-Square Test – Fertilizer Preference by Block
If you want to test **categorical variables** (not numbers):  

```python
import pandas as pd
from scipy.stats import chi2_contingency

fert = pd.crosstab(df["Block"], df["Fertilizer_Type"])
chi2, p_val, dof, expected = chi2_contingency(fert)
print("Chi2:", chi2, "p-value:", p_val)
```
👉 Tests if fertilizer type usage depends on block.  

---

## 18.6 Plantation Case Study – Is Fertilizer Effective?
Management wants to know: *“Did fertilizer significantly improve yields?”*  
- H₀: Fertilizer type doesn’t affect yield.  
- H₁: Fertilizer type does affect yield.  
- Test: Two-sample t-test between MOP and Urea yields.  
- Outcome: Decide if fertilizer procurement strategy should change.  

---

## 18.7 Reflection Questions
1. Why is it dangerous to rely only on averages without testing?  
2. What does a p-value really mean in plain terms?  
3. How could statistical testing prevent wasting money on unnecessary fertilizer?  

---

## 18.8 Practice Exercises

**Exercise 18.1 – Fertilizer Test**  
- Use `estate_dashboard.csv`.  
- Compare MOP vs NPK yields with a t-test.  

**Exercise 18.2 – Labor Productivity**  
- Use `labor.csv` + `block_yields.csv`.  
- Test if blocks with >25 workers produce significantly higher yield than blocks with ≤25 workers.  

**Exercise 18.3 – Chi-Square**  
- Test if fertilizer type usage is independent of block.  

**Exercise 18.4 – Challenge**  
- Simulate yield data for 2 years.  
- Test if average yields in Year 2 are significantly higher than Year 1.  

---

## 18.9 Section Summary
- Hypothesis testing helps **separate real effects from chance**.  
- t-tests compare averages, chi-square tests compare categories.  
- Plantation examples: fertilizer efficiency, labor impact, seasonal differences.  
- Statistical decisions reduce risk of wasting resources.  

**Take-home Challenge:**  
Using `estate_dashboard.csv`:  
1. Test if rainfall significantly affects yield correlation.  
2. Test if Block D’s yields are significantly higher than Block A’s.  
3. Write a recommendation for management: “Which fertilizer should we buy more of next year?”  
