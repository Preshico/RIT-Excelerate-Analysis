# RIT Excelerate — Learner Participation Analysis
### AI Powered Data Analysis Internship | Excelerate x Rochester Institute of Technology

![Python](https://img.shields.io/badge/Python-3.x-blue)
![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-orange)
![XGBoost](https://img.shields.io/badge/XGBoost-Boosting-green)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-lightblue)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

---

## 📌 Project Overview

This project analyzes learner engagement data from the **RIT Excelerate platform** — a programme connecting students with real-world professional opportunities including internships, courses, events, and competitions.

The goal was to understand **why learners apply but do not start**, build a machine learning model to predict the probability of a learner progressing to Started status, and deliver actionable recommendations to improve platform performance.

> *Completed as part of a collaborative AI Powered Data Analysis Internship with Excelerate x RIT. My personal contributions covered data cleaning, exploratory data analysis, report writing, insights, and strategic recommendations.*

---

## 📊 Dataset

| Attribute | Value |
|---|---|
| Source | RIT Excelerate Platform |
| Records | 8,554 learner-opportunity interactions |
| Features | 16 columns (raw) → 11 modelling features |
| Date Range | October 2022 – April 2024 |
| Countries | 71 |
| Institutions | 1,819 |
| Opportunities | 22 across 5 categories |
| Target Variable | Started Flag (1 = Started, 0 = Did not start) |
| Class Balance | 9.3% started / 90.7% not started |

---

## 🎯 Prediction Objective

We predicted the **probability that a learner who has applied for an opportunity will progress to Started status** — enabling early identification of high-potential learners before opportunities close.

- Score close to **1** = high likelihood of starting
- Score close to **0** = unlikely to start

This gives RIT a practical tool to prioritise onboarding support and identify at-risk learners before drop-off happens.

---

## 🗂️ Project Structure

```
RIT-Excelerate-Analysis/
│
├── data/
│   ├── RIT_Opportunity_Wise_Data_Sheet1.csv      # Raw dataset
│   ├── RIT_Cleaned_Final.csv                     # Week 1 cleaned dataset
│   └── RIT_ML_Ready_v2.csv                       # Week 2 ML-ready dataset
│
├── notebooks/
│   ├── Week1_DataUnderstanding.ipynb             # Data cleaning & EDA
│   ├── Week2_EDA_CohortAnalysis.ipynb            # Cohort analysis & features
│   └── Week3_Modeling_Report.ipynb               # ML models & predictions
│
├── outputs/
│   ├── RIT_Predictions_Final.csv                 # Predicted probabilities
│   ├── model_comparison_final.png                # 5-model comparison
│   ├── confusion_matrices_final.png              # All 5 confusion matrices
│   ├── feature_importance_final.png              # Feature importance
│   ├── probability_heatmap_final.png             # Probability heatmap
│   └── opportunity_probabilities_final.png       # Opportunity predictions
│
├── reports/
│   ├── Week1_DataUnderstanding_Report.docx
│   ├── Week2_CohortAnalysis_Report.docx
│   ├── Week3_ModelingReport_Final.docx
│   └── Week4_FinalPresentationReport.docx
│
└── README.md
```

---

## 🔄 Project Workflow

### Week 1 — Data Understanding & Cleaning
- Loaded and inspected 8,558 raw records across 16 columns
- Filled 5 missing values in Institution Name and Current/Intended Major
- Fixed 107 corrupt date timestamps in Apply Date column
- Standardised Institution Name casing — reduced 2,089 variants to 1,819
- Removed 4 fully duplicate rows
- **Final clean dataset: 8,554 rows, 16 columns**

### Week 2 — Exploratory Data Analysis & Feature Engineering
- Conducted cohort analysis across time, geography, gender, age, and opportunity type
- Engineered 8 derived features including **Days Before Close**
- Key finding: start rates collapsed from 89.1% (early 2023) to 0.4% (late 2023–2024)
- Built leakage-free ML-ready dataset removing status-derived features

### Week 3 — Machine Learning & Predictions
- Applied SMOTE to training set only as sole balancing technique
- Trained and evaluated 5 models across different algorithm families
- Selected Random Forest as primary model (ROC-AUC: 0.998, F1: 0.959)
- Generated predicted start probabilities for all 8,554 learners

### Week 4 — Insights & Strategic Recommendations
- Synthesised findings into 5 prioritised recommendations
- Built measurement framework with KPIs, baselines, targets, and timelines
- Delivered final report and presentation to Excelerate and RIT

---

## 🤖 Machine Learning Results

| Model | Precision | Recall | F1-Score | ROC-AUC | Selected |
|---|---|---|---|---|---|
| Logistic Regression | 0.487 | 0.956 | 0.645 | 0.970 | No |
| Decision Tree | 0.925 | 0.931 | 0.928 | 0.962 | No |
| XGBoost | 0.962 | 0.950 | 0.956 | 0.997 | No |
| Gradient Boosting | 0.956 | 0.950 | 0.953 | 0.997 | No |
| **Random Forest** | **0.962** | **0.956** | **0.959** | **0.998** | **✅ YES** |

### Why Random Forest?
Random Forest achieved the highest ROC-AUC (0.998), highest Recall (0.956), and highest F1-Score (0.959) simultaneously. For this use case — where missing a likely starter is the most costly error — Recall was the deciding metric.

---

## 🔍 Key Findings

**Finding 1 — Conversion Crisis**
Applications grew to a record 2,487 in January 2024 while start rates collapsed to 0.4% — down from 89.1% in early 2023. This is a conversion and capacity failure, not a demand problem.

**Finding 2 — Timing is Everything**
Days Before Close accounts for 44% of the Random Forest model's predictive power — more than all demographic features combined. Learners who apply early are dramatically more likely to start.

**Finding 3 — Only 2 Opportunities Work**
Career Essentials (47.3%) and CPR/AED Certification (31.3%) are the only opportunities with meaningful predicted start probabilities. All other 20 fall below 10%.

**Finding 4 — Demographics Don't Predict Participation**
Gender, age, institution, and field of study each contribute less than 1% to model predictions. The platform does not systematically disadvantage any learner demographic.

**Finding 5 — Internship Tracking Gap**
Internships represent 63.3% of all applications. All 5 models predict 0% start probability for this category — suggesting either a conversion failure or a status-tracking gap.

---

## 💡 Recommendations

| Priority | Recommendation | Expected Impact |
|---|---|---|
| 1 | Launch early-application campaign (reminders 4–6 weeks before close) | Directly addresses top predictor |
| 2 | Scale Career Essentials & redesign underperformers | Maximise proven converters |
| 3 | Audit internship status-tracking workflow | Resolve 63% of application volume |
| 4 | Fix onboarding capacity gap from August 2023 | Restore conversion rates |
| 5 | Focus outreach on high-converting markets | Pakistan 41.9% vs US 3.5% |

---

## 📏 Measurement Framework

| KPI | Baseline | Target | Timeline |
|---|---|---|---|
| % applying 4+ weeks before close | Needs audit | 30% of applicants | 3 months |
| Start rate per opportunity | Career Essentials: 46.4% | All core opps >15% | 6 months |
| Internship recorded starts | 0 | > 0 confirmed | 1 month |
| Overall start rate | 0.4% (Oct 23–Apr 24) | > 10% overall | 6 months |
| Start rate — US market | 3.5% | > 8% | 6 months |

---

## 🛠️ Tools & Libraries

```python
# Core
pandas              # Data manipulation
numpy               # Numerical operations
matplotlib          # Visualization
seaborn             # Statistical visualization

# Machine Learning
scikit-learn        # Models, metrics, train-test split
xgboost             # XGBoost classifier
imbalanced-learn    # SMOTE for class balancing

# Models Trained
LogisticRegression
DecisionTreeClassifier
RandomForestClassifier      # Selected model
XGBClassifier
GradientBoostingClassifier
```

---

## 📈 Feature Importance (Random Forest)

| Rank | Feature | Importance | Business Meaning |
|---|---|---|---|
| 1 | Days Before Close | 44.0% | How early a learner applies is the strongest driver |
| 2 | Opportunity Category | 17.2% | Type of opportunity strongly shapes participation |
| 3 | Application Year | 14.0% | Conversion has declined significantly year-on-year |
| 4 | Opportunity Name | 10.2% | Specific opportunity matters — Career Essentials leads |
| 5 | Application Month | 9.4% | Seasonal patterns have moderate influence |
| 6 | Country | 2.2% | Geographic origin has limited but real signal |
| 7+ | Gender, Age, Major | < 1% each | Demographic features have negligible predictive value |

---

## 🚀 How to Run

```bash
# 1. Clone the repository
git clone https://github.com/Preshico/RIT-Excelerate-Analysis.git
cd RIT-Excelerate-Analysis

# 2. Install dependencies
pip install pandas numpy matplotlib seaborn scikit-learn xgboost imbalanced-learn

# 3. Open notebooks in order
jupyter notebook notebooks/Week1_DataUnderstanding.ipynb
jupyter notebook notebooks/Week2_EDA_CohortAnalysis.ipynb
jupyter notebook notebooks/Week3_Modeling_Report.ipynb
```

---

## 📬 Contact

**Precious Ifeoma Ugwu**
- 📧 Email: preciousgiftdgreat@gmail.com
- 💼 LinkedIn: [linkedin.com/in/ifeoma-ugwu-637a17242](https://linkedin.com/in/ifeoma-ugwu-637a17242)
- 🌍 Location: Abuja, Nigeria

---

*This project was completed as part of the Excelerate AI Powered Data Analysis Internship in collaboration with Rochester Institute of Technology (RIT). My personal contributions covered data cleaning, exploratory data analysis, report writing, insights, and strategic recommendations.*
