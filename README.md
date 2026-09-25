# Customer Churn Prediction

This project uses the IBM Telco Customer Churn dataset to identify customers at risk of leaving. I compared logistic regression and random forest models, then examined churn patterns to suggest where a retention team might focus its efforts.

## Dataset

This project uses the [Telco Customer Churn dataset on Kaggle](https://www.kaggle.com/datasets/blastchar/telco-customer-churn), based on IBM sample data. It contains 7,043 customer records. The CSV is included in this repository as `Telco-Customer-Churn.csv`.

## Approach

1. Inspected the data, converted `TotalCharges` to numeric, and prepared categorical variables.
2. Explored churn rates and the relationship between tenure, monthly charges, and total charges.
3. Removed customer ID and `TotalCharges` from the model inputs.
4. Split the data into stratified training and test sets.
5. Used preprocessing pipelines and five-fold cross-validation to compare logistic regression and random forest.
6. Tuned both models using churn recall as the selection metric and evaluated the selected model on the held-out test set.

## Model results

| Model | Cross-validation recall | Precision | F1 | ROC-AUC |
| --- | ---: | ---: | ---: | ---: |
| Tuned logistic regression | 0.796 | 0.513 | 0.624 | 0.842 |
| Tuned random forest | 0.801 | 0.520 | 0.631 | 0.845 |

The tuned random forest scored slightly higher across these measures, so I selected it for final evaluation. The differences were small.

**Held-out test results:** The random forest identified 440 of 561 customers who churned and missed 121. It also flagged 407 customers who did not churn. Its churn recall was **0.78**, precision was **0.52**, and ROC-AUC was **0.843**. This tradeoff matters because retention outreach has a cost.

## Business insights

- Month-to-month customers had a churn rate of 42.7%, compared with 11.3% for one-year contracts and 2.8% for two-year contracts.
- Churn was higher among fiber-optic customers (41.9%) and customers paying by electronic check (45.3%).
- Churn declined across tenure groups, from 52.9% for customers with up to six months of tenure to 6.6% for customers with more than 60 months.

Retention teams could prioritize newer customers and those on month-to-month contracts. The higher churn rates among fiber-optic and electronic-check customers warrant further investigation into service and billing experiences.

These are associations in the dataset, not proof that changing a contract or payment method would prevent churn. Before using the model for outreach, the team should weigh the cost of contacting customers against the value of retaining them.

## Run the notebook

Download or clone this repository, then open `customer-churn-analysis.ipynb` in Jupyter Notebook or another notebook environment. Keep `Telco-Customer-Churn.csv` in the same working directory as the notebook.

The notebook uses pandas, NumPy, Matplotlib, and scikit-learn. Run its cells from top to bottom.

## Repository contents

- `customer-churn-analysis.ipynb` — analysis, model comparison, and findings
- `Telco-Customer-Churn.csv` — dataset
- `README.md` — project summary
