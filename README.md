
# Predicting Driver Attrition for Ola: Ensemble Learning

This project tackles high driver churn at Ola by predicting driver attrition. Using ensemble techniques—bagging (Random Forest) and boosting (XGBoost)—along with KNN imputation, SMOTE, and standard scaling, we analyze demographic, tenure, and performance data to enable proactive retention strategies.

---

## Table of Contents

- [Predicting Driver Attrition for Ola: Ensemble Learning](#predicting-driver-attrition-for-ola-ensemble-learning)
  - [Table of Contents](#table-of-contents)
  - [Project Overview](#project-overview)
  - [Problem Statement](#problem-statement)
  - [Dataset Description](#dataset-description)
  - [Exploratory Data Analysis (EDA)](#exploratory-data-analysis-eda)
  - [Data Preprocessing](#data-preprocessing)
  - [Feature Engineering](#feature-engineering)
  - [Model Building](#model-building)
    - [Bagging: Random Forest](#bagging-random-forest)
    - [Boosting: XGBoost](#boosting-xgboost)
  - [Results Evaluation](#results-evaluation)
  - [Actionable Insights \& Recommendations](#actionable-insights--recommendations)
  - [Repository Structure](#repository-structure)
  - [Technologies \& Their Use](#technologies--their-use)
  - [License](#license)

---

## Project Overview

Ola faces high driver churn, which increases recruitment costs and affects service reliability. This project builds a predictive model using ensemble methods to identify at-risk drivers from monthly historical data. Insights derived from the model help Ola design targeted retention strategies.

---

## Problem Statement

Driver attrition impacts operational efficiency and increases acquisition costs. Our goal is to predict whether a driver will leave Ola based on features including demographics, tenure (joining/last working dates), and performance (quarterly rating, income, business value, and grade). This enables timely, cost-effective retention measures.

---

## Dataset Description

**Dataset:** `ola_driver.csv`

**Key Features:**
- **Demographics:** Age, Gender, City, Education_Level
- **Tenure:** Dateofjoining, LastWorkingDate
- **Performance:** Quarterly Rating, Total Business Value, Income, Grade
- **Target:** Derived attrition indicator (1 if driver left, 0 otherwise)

---

## Exploratory Data Analysis (EDA)

- **Data Inspection:** Reviewed shape (19,104 rows × 14 columns), data types, and missing values.
- **Univariate Analysis:** Plotted histograms for Age, Income, Total Business Value, and Quarterly Rating; countplots for Gender, City, and Education_Level.
- **Bivariate Analysis:** Explored relationships between Age vs. Income and Quarterly Rating vs. Total Business Value.

*Key Insights:*
- Most drivers are aged 30–40; incomes are right-skewed.
- Drivers with higher ratings generally generate more business.
- Significant missing values in LastWorkingDate denote attrition.

---

## Data Preprocessing

- **Missing Values:** 
  - Applied KNN imputation for Age and Gender.
  - Replaced missing LastWorkingDate with "Not Left" (indicating current drivers).
- **Outlier Treatment:** Capped extreme values in Total Business Value using the IQR method.
- **Encoding:** One-hot encoded categorical features (City, Education_Level).
- **Scaling:** Standardized numerical features (Age, Income, Total Business Value).

---

## Feature Engineering

- **New Features:**
  - *Rating_Improved:* 1 if the quarterly rating increased from the previous month.
  - *Income_Improved:* 1 if monthly income increased.
  - *Target:* 1 if LastWorkingDate is not "Not Left" (driver left), else 0.
- **Aggregation:** Grouped data by Driver_ID to consolidate monthly records into a single entry per driver.
- **Correlation Analysis:** Evaluated relationships among features to guide model input selection.

---

## Model Building

### Bagging: Random Forest

- **Method:** Random Forest classifier to reduce variance via ensemble bagging.
- **Steps:** 
  - Applied SMOTE to balance the training set.
  - Trained the model on aggregated, preprocessed data.
- **Performance:** Achieved a robust ROC AUC score with balanced precision and recall.

### Boosting: XGBoost

- **Method:** XGBoost classifier to sequentially improve weak learners.
- **Steps:** 
  - Tuned hyperparameters (n_estimators, learning_rate).
  - Evaluated using ROC AUC, classification report, and confusion matrix.
- **Performance:** Slightly outperformed Random Forest in ROC AUC and recall.

---

## Results Evaluation

- **Metrics:** Evaluated using classification reports, ROC AUC curves, and confusion matrices.
- **Findings:** 
  - Both models performed well, with XGBoost showing a marginal edge.
  - Key metrics indicate a good balance between identifying at-risk drivers and minimizing false positives.

---

## Actionable Insights & Recommendations

- **Retention Strategies:**
  - **High Performers:** Incentivize drivers with consistently high quarterly ratings.
  - **At-Risk Drivers:** Identify drivers with declining income or performance for early intervention.
- **Localized Strategies:** Tailor retention programs based on city-specific attrition patterns.
- **Operational Improvements:** Monitor key predictors (e.g., Total Business Value, Income) to refine retention policies continuously.

---

## Repository Structure


Ola_Driver_Attrition/
├── README.md                           # Project overview and documentation
├── data/
│   └── ola_driver.csv                  # Dataset for the project
├── notebooks/
│   └── ola_driver_attrition_analysis.ipynb  # Jupyter Notebook with EDA, preprocessing, feature engineering, and modeling
├── outputs/
│   └── images/                         # Visualizations (plots, ROC curves, etc.)
├── requirements.txt                    # List of Python dependencies
└── LICENSE                             # Project license (MIT License)
```

---

## How to Run the Project

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/GopalGB/Ola_Driver_Attrition.git
   ```
2. **Navigate to the Directory:**
   ```bash
   cd Ola_Driver_Attrition
   ```
3. **Install Dependencies:**
   ```bash
   pip install -r requirements.txt
   ```
4. **Open the Notebook:**
   - Launch Jupyter Notebook or use Google Colab.
   - Open `notebooks/ola_driver_attrition_analysis.ipynb` and run cells sequentially.
5. **Review Outputs:**
   - Visualizations are available in the `outputs/images/` folder.
   - Export the notebook as PDF for a complete report if required.

---

## Technologies & Their Use

We used **Python** (Pandas, NumPy) for data manipulation, **Matplotlib/Seaborn** for visualization, **Scikit-learn** for KNN imputation, SMOTE, and model evaluation, and **XGBoost/Random Forest** for ensemble learning to predict driver attrition and guide retention strategies.

*Project Description (300 characters):*  
"Using ensemble methods (RandomForest bagging and XGBoost boosting), KNN imputation, SMOTE, and scaling, we predict Ola driver attrition from demographics, tenure, and performance data. This enables targeted retention strategies to minimize churn and reduce acquisition costs."

---

## License

This project is licensed under the MIT License. See the [LICENSE](./LICENSE) file for more details.
