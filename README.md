# Credit Card Default Prediction (Taiwan) 💳
**Course:** CSE374 - Machine Learning Classification Project

## 📌 Project Overview
This project aims to predict the probability of a client defaulting on their credit card payment in the subsequent month based on their demographic data, 6-month repayment history, and bill statement amounts. By identifying high-risk clients, financial institutions can proactively manage credit lines and mitigate potential losses.

## 🗂️ Repository Structure
The project follows a modular, professional architecture separating data assets from executable code:

```text
CreditCardDefault/
│
├── data/
│   ├── raw_data.xls            # Original UCI dataset
│   └── processed_splits.pkl    # Scaled, SMOTE-balanced train/val/test splits
│
├── notebooks/
│   ├── eda.ipynb               # Exploratory Data Analysis & Visualizations
│   ├── preprocessing.ipynb     # Data cleaning, scaling, and SMOTE implementation
│   └── modeling.ipynb          # Model training, hyperparameter tuning, and evaluation
│
├── .gitignore
└── README.md
```

## 📊 Dataset
* **Source:** [Default of Credit Card Clients Dataset (UCI Machine Learning Repository)](https://archive.ics.uci.edu/dataset/350/default+of+credit+card+clients)
* **Size:** 30,000 instances, 23 features.
* **Target Variable:** `default` (Binary: 0 = No Default, 1 = Default).

## ⚙️ Methodology & Pipeline
1. **Data Preprocessing (Role 1):**
   * Cleaned undocumented categorical variables (e.g., in `EDUCATION` and `MARRIAGE`).
   * Scaled all numerical financial features (bill amounts, pay amounts, credit limits) using `StandardScaler` to handle extreme outliers while preventing data leakage.
   * Handled heavy class imbalance (~78% majority) by applying **SMOTE** exclusively to the training set.
2. **Exploratory Data Analysis (Role 2):**
   * Investigated feature distributions and correlation matrices to understand the underlying financial behaviors preceding a default.
3. **Modeling & Evaluation (Role 3):**
   * Implemented and evaluated three classifiers: **Logistic Regression**, **Decision Tree**, and **K-Nearest Neighbors (KNN)**.
   * Prioritized **F1-Score** and **ROC/AUC** over pure accuracy due to the business context (minimizing the cost of false negatives).

## 🏆 Final Results
The **Decision Tree** emerged as the highest-performing model, successfully capturing non-linear interactions in the financial data that linear models and distance-based models missed. Feature importance extraction revealed that `PAY_1` (the most recent repayment status) was the strongest predictor of default.

**Final Unseen Test Set Metrics (Decision Tree):**
* **Accuracy:** 0.7430
* **F1-Score:** 0.4964
* **AUC Score:** 0.7421

*(Note: The relatively high number of False Positives is a deliberate architectural choice resulting from SMOTE balancing, prioritizing the capture of true defaulters over minimizing false alarms).*

## 🚀 How to Run Locally
1. Clone the repository:
   ```bash
   git clone [https://github.com/amrrnagy/CreditCardDefault.git]
   ```
2. Navigate to the `notebooks/` directory.
3. Run `preprocessing.ipynb` from top to bottom. This will generate the `processed_splits.pkl` file in the `/data` folder using relative paths.
4. Run `modeling.ipynb` to load the processed data, train the models, and generate the final confusion matrices and performance metrics.

## 👥 Team Contributions
* **Amr (Project Lead & Role 3):** Modeling & Evaluation Lead (Repository Manager)
* **Yahia (Role 2):** Exploratory Data Analysis (EDA) & Visualization Lead
* **Morshed (Role 1):** Data & Preprocessing Lead
