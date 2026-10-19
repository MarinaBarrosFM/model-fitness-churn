# Model Fitness: Customer Churn Prediction and Segmentation

A data-driven retention study for **Model Fitness**, a gym chain that wants to reduce customer churn. Using data on 4,000 customers, the project predicts who is likely to leave, groups customers into behavioral segments, and turns the findings into practical retention actions.

## Business questions
1. Which customer characteristics are associated with churn?
2. Can we predict which customers will leave next month?
3. Are there natural customer segments, and do they differ in churn rate?
4. What should the company do to retain customers?

## Data
`gym_churn_us.csv`: 4,000 customers and 14 columns (13 features plus the target `Churn`), with no missing values. Features include gender, proximity to the gym, partner-company membership, friend-referral promo, contract period, group-class attendance, age, additional spending, months to contract end, lifetime (months), visit frequency, and the `Churn` flag.

> The dataset comes from the TripleTen Data Analyst bootcamp and is not included in this repository.

## Approach
- **Exploratory data analysis:** descriptive statistics, feature means for churned vs. retained customers, distributions by group, and a correlation matrix.
- **Churn prediction:** binary classification with **Logistic Regression** and **Random Forest** (80/20 train/validation split, features standardized using the training set only), evaluated with accuracy, precision and recall.
- **Customer segmentation:** hierarchical clustering (dendrogram) to explore the number of clusters, then **K-means with 5 clusters**, excluding the churn column.
- **Business recommendations** based on the model and cluster profiles.

## Key results
| Model | Accuracy | Precision | Recall |
|---|---|---|---|
| Logistic Regression | 0.92 | 0.85 | 0.83 |
| Random Forest | 0.92 | 0.84 | 0.81 |

Recall is the priority metric, since the goal is to identify customers who are about to leave. The two models perform very similarly, with logistic regression slightly ahead and easier to interpret.

**Findings**
- Churn happens early: churned customers have on average about **1 month** of tenure vs. 4.7 months for retained customers, and shorter contracts (about 1.7 vs. 5.75 months).
- **Visit frequency is the strongest warning sign:** churned customers visit about 1.04 times per week in the current month vs. 2.03 for retained customers.
- Social ties protect against churn: retained customers attend more group classes (46% vs. 27%), come more often from partner companies (53% vs. 36%) and friend referrals (35% vs. 18%), and spend more on additional services.
- Gender and having provided a phone number show little influence.

**Customer segments (K-means, 5 clusters)**

| Cluster | Customers | Churn rate |
|---|---|---|
| 3 | 1,262 | 51% |
| 2 | 505 | 44% |
| 1 | 385 | 27% |
| 4 | 838 | 7% |
| 0 | 1,010 | 3% |

Cluster 3 (short contracts, youngest, lowest attendance) is the top retention priority. Cluster 2 groups customers who live far from the gym. Clusters 0 and 4 are the most loyal.

**Recommendations:** a welcome program for the first two months, frequency-based alerts for customers dropping below about one visit per week, converting short contracts into longer ones, strengthening group classes, friend referrals and corporate partnerships, flexible plans for customers who live far away, and alternative contact channels for customers without a phone number.

## Tools
Python, pandas, NumPy, scikit-learn, SciPy, Matplotlib and Seaborn.

## Files
- `Model_Fitness_Churn.ipynb`: full analysis with outputs. The analysis text is in Portuguese.
