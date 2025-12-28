#  Concert Crowd Energy Prediction & Revenue Optimization

##  Project Overview

This project analyzes live concert data to **predict Crowd Energy levels** and **optimize ticket pricing** to maximize profit for a specific venue (**V_Gamma – “The Snob Pit”**).

The work combines:

* Exploratory Data Analysis (EDA)
* Machine Learning (Regression)
* Model validation & leakage control
* Business-driven revenue optimization through simulation

---

##  Repository Structure

```
.
├── analysis_notebook.ipynb        # Complete EDA, modeling, validation & simulations
├── findings_report.pdf            # Key insights, plots, and model findings
├── revenue_optimization.pdf       # Business-focused optimization & pricing analysis
├── predictions.csv                # Final test-set predictions (Gig_ID, Crowd_Energy)
├── README.md                      # Project overview (this file)
```

---

##  Problem Statement

* Predict **Crowd_Energy (0–100)** for live gigs
* Use predictions to **optimize ticket pricing** at Venue **V_Gamma**
* Account for real-world constraints

---

## 📊 Data Summary

Each gig contains:

* Ticket_Price
* Crowd_Size
* Volume_Level
* Venue (One-Hot Encoded)
* Time & Date features
* Weather & other Band attributes also

Detailed info is avaialable in `analysis_notebook.ipynb`

Target:

* **Crowd_Energy**

All features used in the final model are **numerical**.

---

## 🔍 Exploratory Data Analysis

Key insights:

* Crowd Energy varies strongly by **venue**
* Crowd size and energy have **weak direct correlation**
* Extreme values and data leakage sources were identified and removed

Detailed analysis and plots are available in:

* `analysis_notebook.ipynb`
* `findings_report.pdf`

---

## 🤖 Model Choice & Justification

### **Random Forest Regressor**

Chosen because it:

* Captures **non-linear relationships**
* Is robust to noise and outliers
* Requires minimal distributional assumptions
* Performs well on mixed behavioral features

---

## ⚙️ Model Training & Validation

### Validation Strategy

* **5-fold cross-validation**
* Metric: **RMSE (Root Mean Squared Error)**

### Performance

| Model                 | CV RMSE   |
| --------------------- | --------- |
| Venue Median Baseline | ~14.94     |
| Tuned Random Forest   | **~12.69** |

This represents a **significant improvement over baseline**.

Overfitting checks:

* Train RMSE ≈ CV RMSE
* Residual plots show no strong systematic bias

---

##  Hyperparameter Tuning

Hyperparameters explored:

* `n_estimators`
* `max_depth`
* `min_samples_leaf`
* `min_samples_split`
* `max_features`

Tuning method:

* **RandomizedSearchCV**
* Justification: better exploration of large search space

Final parameters selected based on **lowest average CV RMSE**, not training error.

---

##  Revenue Optimization (Bonus Objective)

### Business Context (V_Gamma)

* Capacity: ~800 seats
* Fixed cost: ~$5,000
* Variable cost: ~$8 per attendee

### Profit Formula

$$\text{Profit} = (\text{Attendance} \times \text{Ticket Price}) - (5000 + 8 \times \text{Attendance})$$

### Method

1. Use trained model to **predict Crowd Energy** (without using crowd size as a driver)
2. Convert predicted energy → attendance using empirical calibration
3. Simulate profit across ticket prices
4. Identify optimal pricing zone

Results and justification are detailed in:

* `revenue_optimization.pdf`

---

##  Key Outcome

* Optimal ticket pricing lies in a **mid-range zone**, not at extremes
* Very high prices reduce energy → attendance → profit
* Crowd energy is **venue-dependent**, justifying higher weight for V_Gamma

---

##  Final Outputs

* **Predictions:** `predictions.csv`
* **Technical Analysis:** `analysis_notebook.ipynb`
* **Findings Summary:** `findings_report.pdf`
* **Business Optimization:** `revenue_optimization.pdf`

---

##  How to Run

1. Open `analysis_notebook.ipynb`
2. Run cells top to bottom
3. Final predictions will be generated as `predictions.csv`

---

##  Notes

* All preprocessing applied **consistently** to train & test
* No target leakage used in final model
* Model is robust to distribution shifts and unseen combinations

---

##  Author

* **Divyam**
* First Year student at IIT Guwahati in CSE Department
* Machine Learning & Data Analysis Project
