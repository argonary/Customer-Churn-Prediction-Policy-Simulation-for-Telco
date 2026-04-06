\# Customer Churn Prediction and Policy Simulation | Telecom Sector



View Interactive Notebook: https://argonary.github.io/Customer-Churn-Prediction-Policy-Simulation-for-Telco/



\## Objective



Build a transparent, end-to-end churn prediction system that quantifies model

signal, evaluates cost-benefit tradeoffs, and translates churn probabilities

into actionable retention policies for a telecom operator.



\## Project Structure



| Section | Purpose |

|:--|:--|

| 1. Setup and Data Load | Deterministic configuration, data import, MLflow tracking setup |

| 2. Schema Audit | Validate completeness, missingness, and class balance |

| 3. Cleaning and Imputation | Tenure-bin median imputation, type coercion |

| 4. Feature Engineering | Leak-safe features: tenure transforms, charge gaps, behavioral flags |

| 5. Feature Audit | Mutual information, Spearman correlation, VIF, permutation importance |

| 6. Segmentation | K-Means clustering with automated cluster narratives |

| 7. Modeling Leaderboard | Repeated cross-validation across LogReg, GB, XGBoost logged in MLflow |

| 8. Policy Selection | Precision/recall tradeoff for 15% vs 20% outreach quotas |

| 9. Ops Handoff | Scored CSV with dual policy flags for CRM integration |

| 10. Documentation | Executive summary and ROI projection |



\## Key Results



| Model | ROC-AUC | PR-AUC |

|:--|:--|:--|

| Gradient Boosting | 0.844 +/- 0.009 | 0.653 +/- 0.023 |

| Logistic Regression | 0.843 +/- 0.010 | 0.647 +/- 0.025 |

| XGBoost | 0.817 +/- 0.009 | 0.596 +/- 0.021 |



Gradient Boosting was selected based on PR-AUC, the appropriate metric for

imbalanced classification. While ROC-AUC is nearly identical across GB and LR,

GB wins more clearly on PR-AUC and captures non-linear feature interactions

that logistic regression cannot express without manual interaction terms.



| Policy | Precision | Recall | Notes |

|:--|:--|:--|:--|

| 15% outreach | 0.692 | 0.391 | Cost-efficient, high-confidence contacts |

| 20% outreach | 0.657 | 0.495 | Recommended operational policy |



The 20% policy recovers roughly 25% more churners for only 4 percentage points

of precision loss, making it the better balance between cost and coverage.



\## Projected Business Impact



Based on the 20% outreach policy, with a 30% retention campaign success rate

and average monthly revenue of 65 USD per customer, the model projects

approximately 217,000 USD in retained revenue per campaign cycle. At scale

across a customer base 10x this size, or with higher average revenue per user

typical of enterprise telecom contracts, the projection reaches 1-2M USD

annually.



\## Key Insights



\- Contract type is the strongest churn signal. Month-to-month customers churn

&#x20; at dramatically higher rates than one or two year contract holders.

\- Tenure is strongly protective. Short-tenure customers drive the majority of

&#x20; churn risk across all model and SHAP analyses.

\- Fiber optic internet service customers show elevated churn risk despite being

&#x20; high-value, suggesting a service quality or pricing issue worth investigating.

\- Feature engineering added real signal. PayRisk and M2M\_x\_tenurebin both

&#x20; appear in the top 10 SHAP features, confirming that combining payment method

&#x20; and contract type captures behavioral risk that raw features miss.

\- Cluster 0 (48% churn rate) and Cluster 3 (35% churn rate) are the primary

&#x20; retention targets and represent the highest-priority segment for the ops

&#x20; handoff.



\## Segmentation Summary



K-Means clustering evaluated k from 2 to 8 using inertia and silhouette score.

k=4 was selected as the best balance between statistical separation and

business interpretability, producing four actionable customer segments with

churn rates ranging from 17% to 48% against a dataset baseline of 26.5%.



\## Deliverables



\- handoff\_scored.csv: ranked list of all 7,043 customers with churn

&#x20; probabilities, dual policy flags, cluster assignment, and key business context

\- reports/plots/leaderboard\_plot.html: interactive model leaderboard

\- mlruns\_telco/: MLflow experiment logs and artifacts



\## Tech Stack



\- Python 3.11

\- pandas, numpy, scikit-learn, xgboost, shap

\- plotly, mlflow

\- JupyterLab



\## Setup



1\. Clone the repo

2\. Install dependencies: pip install -r requirements.txt

3\. Run the notebook top to bottom: Final Telco Code.ipynb

4\. Outputs will be written to handoff\_scored.csv and reports/



\## Author



Aryan Pai

MS Business Analytics, UT Austin McCombs

