# Section 7: Mini Project (Capstone) – **Estate Performance Intelligence**

> **Difficulty:** Advanced beginner → Intermediate  
> **Duration:** 90 minutes (can stretch to 2–3 hours with extensions)  
> **Goal:** Integrate everything from Sections 1–6 to build a small, reusable **Python analysis toolkit** for a palm oil estate.

---

## 7.1 Business Scenario

You are the data/operations analyst for **FGV Palm Estate – Segamat Cluster**. Management wants an **evidence‑based performance review** across 4 blocks for the last 12 months and a **repeatable script** they can run monthly. Your job is to:
1. Clean and structure the data (lists/dicts).
2. Compute core KPIs (Yield per Hectare, Labor Productivity, Cost per Tonne).
3. Classify block performance using business rules.
4. Flag anomalies (e.g., sudden yield drops, suspicious fertilizer usage).
5. Produce a **plain‑text summary report** suitable for email/WhatsApp.
6. (Extension) Simulate **“what‑if”** scenarios (e.g., fertilizer cuts, labor changes).

> **Constraints:** Use only Python standard library. No external packages.

---

## 7.2 Data Provided (12 Months × 4 Blocks)

**Blocks:** A, B, C, D  
**Units:** rainfall (mm), area (hectares), workers (count), fertilizer_kg (kg), ffb_tonnes (tonnes), ripeness_rate (%), pest_incidents (count)

> Treat `area` as static per block, while the rest vary monthly.

```text
AREA (static):
Block A:  10.5 ha
Block B:  12.0 ha
Block C:  11.0 ha
Block D:  13.0 ha
```

### Monthly Panel (Jan–Dec)
> Feel free to paste these into your Python file as lists/dicts. Values are realistic but simplified for learning.

```text
MONTHS = ["Jan","Feb","Mar","Apr","May","Jun","Jul","Aug","Sep","Oct","Nov","Dec"]

RAIN_MM = {
  "A": [185,210,198,240,260,190,175,220,205,230,215,200],
  "B": [200,205,215,250,255,210,195,235,220,245,225,210],
  "C": [170,180,190,205,215,185,160,195,200,210,205,190],
  "D": [210,225,235,260,270,220,205,240,230,255,240,225]
}

WORKERS = {
  "A": [12,12,12,13,13,12,11,12,12,13,13,12],
  "B": [15,15,16,16,16,15,14,15,15,16,16,15],
  "C": [13,13,13,13,13,12,12,12,12,13,13,12],
  "D": [17,17,17,18,18,17,16,17,17,18,18,17]
}

FERTILIZER_KG = {
  "A": [200, 220, 220, 250, 260, 210, 180, 230, 220, 240, 230, 220],
  "B": [240, 250, 260, 280, 290, 250, 220, 260, 255, 270, 265, 250],
  "C": [180, 190, 200, 210, 220, 190, 170, 200, 195, 205, 200, 190],
  "D": [260, 270, 280, 300, 320, 270, 240, 290, 285, 300, 295, 280]
}

FFB_TONNES = {
  "A": [24.5,26.0,25.8,27.2,28.0,24.7,22.5,26.3,25.6,27.0,26.1,25.0],
  "B": [29.0,29.5,30.2,31.5,32.0,29.8,27.9,30.8,30.0,31.2,30.5,29.6],
  "C": [22.0,22.5,23.4,24.0,24.6,22.8,20.9,23.0,23.2,24.1,23.7,22.6],
  "D": [31.5,32.4,33.1,34.6,35.3,32.8,30.6,33.7,33.0,34.4,33.8,32.5]
}

RIPENESS_RATE = {  # measured as percentage of ripe bunches at harvest
  "A": [88, 89, 90, 91, 92, 89, 87, 90, 90, 92, 91, 90],
  "B": [90, 90, 91, 92, 93, 91, 89, 92, 92, 93, 92, 91],
  "C": [85, 86, 87, 88, 89, 86, 84, 87, 87, 88, 87, 86],
  "D": [91, 92, 93, 94, 95, 93, 91, 94, 94, 95, 94, 93]
}

PEST_INCIDENTS = {  # monthly logged cases
  "A": [2,1,1,0,0,1,2,1,1,0,1,1],
  "B": [1,1,0,0,0,1,1,0,0,0,1,1],
  "C": [3,3,2,2,2,3,4,3,2,2,2,3],
  "D": [1,0,0,0,0,1,1,0,0,0,1,1]
}
```

---

## 7.3 KPIs & Business Rules

**Static mapping:**
```text
AREA = {"A": 10.5, "B": 12.0, "C": 11.0, "D": 13.0}
```

**KPIs (compute monthly & annual):**
- **Yield per Hectare (YPH)**: `ffb_tonnes / area`
- **Labor Productivity (tonnes/worker)**: `ffb_tonnes / workers`
- **Cost per Tonne (proxy)**: assume **labor_cost_per_worker = 1200** and **fertilizer_cost_per_kg = 2.5**  
  `cost = workers * labor_cost_per_worker + fertilizer_kg * fertilizer_cost_per_kg`  
  `cost_per_tonne = cost / ffb_tonnes`

**Performance Classification (monthly):**
- **YPH target:** ≥ **2.3** tonnes/ha/month → “Good” else “Poor”  
- **Labor productivity target:** ≥ **2.0** tonnes/worker/month → “Efficient” else “Inefficient”  
- **Ripeness threshold:** ≥ **90%** → “Optimal” else “Suboptimal”  
- **Pest incidents:** ≥ **3** → “High risk” (flag block for IPM check)

> You may tune thresholds if your estate norms differ. Keep them consistent across the analysis.

---

## 7.4 Tasks (What Students Must Deliver)

1. **Data Structures**
   - Store the monthly data using **dictionaries of lists** (already given). Recreate them in your `.py` file.
   - Store `AREA` as a separate dictionary.

2. **Helper Functions**  
   Write and use functions (place these near the top of your file):
   - `yph(tonnes, area)` → float  
   - `labor_prod(tonnes, workers)` → float  
   - `cost_per_tonne(workers, fert_kg, tonnes, labor_cost=1200, fert_cost=2.5)` → float  
   - `classify(value, threshold, label_true, label_false)` → str  
   - `block_month_summary(block, month_index)` → returns a **dictionary** with all computed KPIs + labels for that block-month

3. **Compute Monthly & Annual KPIs**
   - For each block (A–D) and month (Jan–Dec), compute all KPIs and classifications.  
   - Aggregate **annual** results per block: average YPH, average labor productivity, average cost/tonne, total pest incidents, average ripeness.

4. **Anomaly Detection**
   - Flag any month where:
     - `ffb_tonnes` drops **> 15%** vs previous month, **and** rainfall did **not** drop > 15% (suspicious).  
     - `fertilizer_kg` increases **> 20%** month‑on‑month but **YPH** decreases (possible inefficiency).

5. **Text Report (Plain Console Output)**
   - Print a **monthly line** like:  
     `Mar – Block B | YPH: 2.52 | Prod: 1.89 | Cost/t: 97.25 | Ripeness: Optimal | Pest: Low`
   - End with a **block‑level annual summary** (averages, totals) and **flags** (anomalies).

6. **What‑If Simulator (Extension)**
   - Accept user inputs via `input()` for:  
     - `% change in workers` (e.g., `-10` for 10% reduction)  
     - `% change in fertilizer_kg`  
   - Recompute **annual KPIs** and show projected changes per block.

7. **(Optional) CLI Experience**
   - Create a simple menu:  
     1) Show monthly report  
     2) Show annual summary  
     3) Run what‑if simulator  
     4) Exit

---

## 7.5 Starter Template (Students Can Copy/Paste)

```python
MONTHS = ["Jan","Feb","Mar","Apr","May","Jun","Jul","Aug","Sep","Oct","Nov","Dec"]
AREA = {"A": 10.5, "B": 12.0, "C": 11.0, "D": 13.0}

# Paste RAIN_MM, WORKERS, FERTILIZER_KG, FFB_TONNES, RIPENESS_RATE, PEST_INCIDENTS here

def kpi_round(x):
    return float(f"{x:.2f}")

def yph(tonnes, area):
    return tonnes / area

def labor_prod(tonnes, workers):
    return tonnes / workers

def cost_per_tonne(workers, fert_kg, tonnes, labor_cost=1200, fert_cost=2.5):
    cost = workers * labor_cost + fert_kg * fert_cost
    return cost / tonnes

def classify(value, threshold, label_true, label_false):
    return label_true if value >= threshold else label_false

def pct_change(curr, prev):
    return (curr - prev) / prev * 100.0

def block_month_summary(block, i):
    tonnes = FFB_TONNES[block][i]
    area = AREA[block]
    workers = WORKERS[block][i]
    fert = FERTILIZER_KG[block][i]
    rain = RAIN_MM[block][i]
    ripe = RIPENESS_RATE[block][i]
    pests = PEST_INCIDENTS[block][i]

    kpi_yph = yph(tonnes, area)
    kpi_prod = labor_prod(tonnes, workers)
    kpi_cpt = cost_per_tonne(workers, fert, tonnes)
    label_yph = classify(kpi_yph, 2.3, "Good", "Poor")
    label_prod = classify(kpi_prod, 2.0, "Efficient", "Inefficient")
    label_ripe = classify(ripe, 90, "Optimal", "Suboptimal")
    label_pest = "High risk" if pests >= 3 else "Low"

    return {
        "month": MONTHS[i], "block": block,
        "tonnes": kpi_round(tonnes), "yph": kpi_round(kpi_yph),
        "prod": kpi_round(kpi_prod), "cost_per_tonne": kpi_round(kpi_cpt),
        "ripeness": ripe, "pests": pests,
        "label_yph": label_yph, "label_prod": label_prod,
        "label_ripeness": label_ripe, "label_pest": label_pest
    }

def detect_anomalies(block):
    notes = []
    for i in range(1, 12):
        t_curr, t_prev = FFB_TONNES[block][i], FFB_TONNES[block][i-1]
        r_curr, r_prev = RAIN_MM[block][i], RAIN_MM[block][i-1]
        f_curr, f_prev = FERTILIZER_KG[block][i], FERTILIZER_KG[block][i-1]

        drop_t = pct_change(t_curr, t_prev) < -15
        drop_r = pct_change(r_curr, r_prev) < -15
        fert_up = pct_change(f_curr, f_prev) > 20

        if drop_t and not drop_r:
            notes.append(f"{MONTHS[i]}: Yield drop >15% without rain drop – investigate operations/logistics.")
        if fert_up and t_curr < t_prev:
            notes.append(f"{MONTHS[i]}: Fertilizer up >20% but yield fell – check application timing/quality.")
    return notes

def monthly_report():
    for i in range(12):
        for block in ["A","B","C","D"]:
            s = block_month_summary(block, i)
            print(f"{s['month']} – Block {block} | YPH: {s['yph']} | Prod: {s['prod']} | Cost/t: {s['cost_per_tonne']} | Ripeness: {s['label_ripeness']} | Pest: {s['label_pest']}")

def annual_summary():
    for block in ["A","B","C","D"]:
        yph_list, prod_list, cpt_list, pests_total, ripe_list = [], [], [], 0, []
        for i in range(12):
            s = block_month_summary(block, i)
            yph_list.append(s['yph'])
            prod_list.append(s['prod'])
            cpt_list.append(s['cost_per_tonne'])
            pests_total += s['pests']
            ripe_list.append(s['ripeness'])
        anomalies = detect_anomalies(block)
        print("")
        print(f"Block {block} – Annual Summary")
        print(f"  Avg YPH: {kpi_round(sum(yph_list)/len(yph_list))}")
        print(f"  Avg Productivity: {kpi_round(sum(prod_list)/len(prod_list))}")
        print(f"  Avg Cost/t: {kpi_round(sum(cpt_list)/len(cpt_list))}")
        print(f"  Avg Ripeness: {kpi_round(sum(ripe_list)/len(ripe_list))}%")
        print(f"  Total Pest Incidents: {pests_total}")
        print("  Anomalies:")
        for note in anomalies:
            print(f"    - {note}")

if __name__ == "__main__":
    while True:
        print("\n1) Monthly report\n2) Annual summary\n3) Exit")
        choice = input("Choose: ").strip()
        if choice == "1":
            monthly_report()
        elif choice == "2":
            annual_summary()
        elif choice == "3":
            break
        else:
            print("Invalid choice.")
```

> This template is intentionally incomplete (datasets omitted in the code block). Students must paste the datasets from **7.2** and test their functions.

---

## 7.6 Grading / Evaluation Rubric (Instructor Use)

| Criterion | Excellent (A) | Good (B) | Satisfactory (C) | Needs Work (D) |
|---|---|---|---|---|
| Correctness | All KPIs & rules correct, clean outputs | Minor rounding/threshold issues | Several mistakes but runnable | Many errors; logic incorrect |
| Code Quality | Clear functions, good names, comments | Some functions; OK names | Minimal abstraction | Copy‑pasted logic, hard to read |
| Robustness | Handles edge cases, safe division | Few defensive checks | Occasional crashes | Crashes on common inputs |
| Insight | Flags meaningful anomalies; interprets | Some flags, limited insight | Flags present; little narrative | No analysis |
| Presentation | Clean, readable report | Adequate formatting | Messy but legible | Hard to follow |

---

## 7.7 Extension Ideas (For Fast Groups)

- Add **classification tiers** (Gold/Silver/Bronze) based on combined KPI score.  
- Add **moving average** KPIs (3‑month windows).  
- Add **profit proxy**: price_per_tonne × tonnes − cost.  
- Build a **CSV exporter** that writes monthly results to a file.  
- Implement a **what‑if simulator** that scales `WORKERS` and `FERTILIZER_KG` by user‑provided percentages and recomputes annual KPIs.

---

## 7.8 Reflection (Students)

1. Which KPI shifted most across blocks, and why?  
2. Which anomaly flags appeared? Are they operational or data‑quality issues?  
3. What minimal extra data (e.g., vehicle downtime, road condition, mill queue times) would most improve your model?

---

### End of Section 7
Build the script so supervisors can run it at month‑end and understand performance in under a minute.
