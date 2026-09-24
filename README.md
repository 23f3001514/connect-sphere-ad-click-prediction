# Predictive Modeling for Click-Through Rate Optimization at ConnectSphere Digital

A logistic regression model that predicts whether a user will click an online advertisement, so ad budget can be directed at the users most likely to engage.

## Problem

ConnectSphere Digital spends a large share of its ad budget on users with a low probability of engagement, which weakens campaign performance and Return on Ad Spend (ROAS). This project builds a data-driven way to identify and prioritize likely clickers.

## Dataset

`data/advertising.csv` has 1,000 users and 10 columns: Daily Time Spent on Site, Age, Area Income, Daily Internet Usage, Ad Topic Line, City, Male, Country, Timestamp, and the target **Clicked on Ad**. There are no missing values or duplicates, and the classes are perfectly balanced (500 / 500).

## Approach

1. Data quality checks (missing values, duplicates, class balance)
2. Exploratory analysis (distributions, boxplots, correlations, click rate by hour and weekday)
3. Feature engineering: Hour, Month and DayOfWeek extracted from Timestamp
4. Dropped high-cardinality text columns (Ad Topic Line, City, Country)
5. Stratified 80/20 train-test split, `StandardScaler` fitted on training data only
6. Logistic regression, evaluated with accuracy, precision, recall, F1, ROC-AUC and average precision

## Results (200-user test set)

| Metric | Score |
|---|---|
| Accuracy | 0.9800 |
| Precision | 0.9898 |
| Recall | 0.9700 |
| F1-score | 0.9798 |
| ROC-AUC | 0.9915 |
| Average precision | 0.9935 |

Confusion matrix: 99 true negatives, 1 false positive, 3 false negatives, 97 true positives.

## Key findings

- The strongest predictors are Daily Time Spent on Site, Daily Internet Usage, Area Income and Age.
- Heavy site and internet users click less. Older users click more.
- Hour, month, day of week and gender add very little signal.

## Limitations

The test set is small and the data is unusually clean (50% click rate). Real campaigns typically have far lower CTR and class imbalance. Cross-validation and an A/B test are recommended before deployment.

## Repository structure

```
├── data/advertising.csv
├── notebooks/CTR_advertisement.ipynb
├── reports/ConnectSphere_CTR_Project_Report.pdf
└── requirements.txt
```

## How to run

```bash
git clone https://github.com/23f3001514/ctr-prediction-logistic-regression.git
cd ctr-prediction-logistic-regression
pip install -r requirements.txt
jupyter notebook notebooks/CTR_advertisement.ipynb
```

## Tech stack

Python, pandas, NumPy, scikit-learn, matplotlib, seaborn
