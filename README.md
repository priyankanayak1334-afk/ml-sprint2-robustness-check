# ml-sprint2-robustness-check
# Sprint 2 Review: Model Robustness & Feature Degradation Challenge

## 🎯 Project Overview
This repository contains the Sprint 2 engineering deliverables focused on validating model performance under sudden real-world data constraints. 

In production environments, upstream pipeline shifts can cause critical features to disappear, degrade, or introduce excessive noise. This experiment evaluates system resilience by systematically isolating the primary predictor, dropping it from the pipeline, and retraining the core model architecture from scratch to evaluate fallback stability.

---

## 📊 Performance Matrix (Before vs. After Feature Drop)

The table below demonstrates how the system metrics shifted once the most prominent data feature was extracted from the training matrix:

| Evaluation Metrics | Before Drop (Baseline Model) | After Drop (Adapted Model) | Performance Net Change (%) |
| :--- | :---: | :---: | :---: |
| **R² Score** (Higher is Better) | 0.8037 | 0.8194 | **+1.9560%** |
| **Mean Absolute Error (MAE)** (Lower is Better) | 0.3303 | 0.3131 | **-5.2268%** |

---

## 🔍 System Adaptation Analysis

* **Surrogate Feature Elevation:** Rather than collapsing or suffering metric degradation, the model performance experienced a notable optimization boost. The R² score increased by approximately **1.96%** while the absolute prediction error (MAE) decreased by **5.23%**. 
* **Redundancy & Multi-collinearity:** This response indicates that the dropped feature was highly correlated with other variables in the dataset (multi-collinearity), which was causing the baseline model to overfit or absorb unnecessary noise. When dropped, the remaining surrogate features seamlessly stepped up to explain the target variance in a cleaner, more generalized manner.

---

## 🔄 Sprint 2 Engineering Reflection

* **What Went Well:** The modular pipeline architecture allowed for rapid retraining and validation tracking without breaking state configurations. Incorporating runtime validation checks prevented execution errors when altering data shapes mid-sprint.
* **Unexpected Dynamics:** Dropping what appeared to be the "most important feature" based on initial tree splits resulted in a better-performing model. This highlights a critical ML lesson: high feature importance scores do not always equate to structural necessity if the feature introduces information redundancy.
* **Sprint 3 Action Plan:** Moving forward into Sprint 3, we will implement systematic **Recursive Feature Elimination (RFE)** and generate cross-correlation matrices during the exploratory phase to prune noisy or redundant features *before* baseline deployment.

---

## 🛠️ How to Replicate the Experiment

1. Clone this repository locally:
   ```bash
   git clone https://github.com
   ```
2. Open the project workspace and launch your local environment:
   ```bash
   jupyter notebook
   ```
3. Open `Untitled78.ipynb` (or your renamed notebook file) and select **Kernel > Restart & Run All** to reproduce the data split, baseline model construction, feature drop execution, and final metrics generation.
