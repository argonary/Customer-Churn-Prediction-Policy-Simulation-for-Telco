# Customer-Churn-Prediction-Policy-Simulation-for-Telco

## Objective

Develop a transparent, data-driven churn prediction system that quantifies model signal, evaluates cost–benefit tradeoffs, and translates churn probabilities into actionable retention policies (e.g., top 15% vs. 20% outreach).

---

## Project Structure

| Section | Purpose |
|----------|----------|
| **0–1. Setup & Data Load** | Deterministic configuration, data import, MLflow tracking setup. |
| **2. Schema Audit** | Validate completeness, missingness, and class balance. |
| **3. Cleaning & Imputation** | Deterministic fixes by tenure bins; type coercion. |
| **4. Feature Engineering** | Curated leak-safe features (tenure transforms, charge gaps, behavioral flags). |
| **5. Feature Audit** | Mutual information, correlation, VIF, permutation importance. |
| **6. Segmentation** | K-Means profiles (contract, internet service, churn behavior). |
| **7. Modeling Leaderboard** | Repeated cross-validation (LogReg, GB, XGB) logged in MLflow. |
| **8. Policy Selection** | Precision/recall trade-off for 15% vs. 20% outreach. |
| **9. Ops Handoff** | Generates `handoff_scored.csv` with dual policy flags and key descriptors. |
| **10. Documentation** | Executive summary and cluster narratives for reporting. |

---

## Tech Stack
- **Languages:** Python 3.11, SQL  
- **Libraries:** pandas, scikit-learn, xgboost, plotly, mlflow  
- **Environment:** JupyterLab / Power BI integration for visualization  
- **Tracking:** MLflow local file backend (`mlruns_telco/`)

---

## Key Results

| Metric | Gradient Boosting | Logistic Regression | XGBoost |
|:--|:--:|:--:|:--:|
| ROC-AUC | 0.844 ± 0.009 | 0.843 ± 0.010 | 0.818 ± 0.009 |
| PR-AUC | **0.653 ± 0.023** | 0.647 ± 0.025 | 0.599 ± 0.021 |

| Policy | Precision | Recall | Notes |
|:--|:--|:--|:--|
| **15%** | 0.692 | 0.391 | Cost-efficient, high-confidence contacts. |
| **20%** | **0.657** | **0.495** | Balanced coverage; recommended operational policy. |

---

## Insights
- **Top drivers of churn:** Contract type, InternetService, tenure_bin, M2M_x_tenurebin, PriceShockPct.  
- **High-risk segments:** Month-to-month Fiber customers with low family support and few add-ons.  
- **Low-risk segments:** Long-tenure bundled customers with multiple add-ons and stable bills.

---

## Deliverables
- `reports/results/handoff_scored.csv` — scored list with churn probabilities and policy flags  
- `reports/plots/leaderboard_plot.html` — model leaderboard visualization  
- `mlruns_telco/` — MLflow experiment logs and artifacts  
- `README.md` — project documentation and summary

---

## Next Steps
1. Integrate `handoff_scored.csv` into CRM outreach systems.  
2. Track retention ROI against modeled precision/recall benchmarks.  
3. Extend feature set with usage, billing, and engagement data for model v2.  
4. Deploy Streamlit dashboard for live churn monitoring.

---

### Author
**Aryan Pai**  
MS Business Analytics, UT Austin McCombs  
Data Science | Machine Learning | Business Strategy
