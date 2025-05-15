
# 🧠 Customer Segmentation for Marketing Offer Strategy

This project segments travel customers into distinct behavioral clusters using SQL for data preparation and Python for machine learning. Our goal is to support data-driven marketing strategies with actionable insights and targeted offers.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/marinaG1717/Tide-Travel-Project/blob/main/notebooks/customer_segmentation.ipynb)
---

## 🎯 Project Goal

Segment customers based on:

- Booking behavior
- Travel intensity
- Spending patterns
- Discount sensitivity

### 🔍 Key Business Questions:
- Who are the frequent travelers?
- Who is highly sensitive to discounts?
- Who spends the most?
- Who just browses?

---

## 🧱 Tech Stack

- **SQL**: Data extraction, transformation, and aggregation (via Beekeeper Studio, NeonDB)
- **Python**: Clustering (Pandas, Scikit-learn, Seaborn, etc.) 
- **Jupyter Notebook**: EDA and model training  ([notebooks/tide_travel_clustering.ipynb`](notebooks/tide_travel_clustering.ipynb))
- **K-Means Clustering**: Primary algorithm
- **Silhouette Score**: `0.29` (adequate for business interpretation)

---

## 📦 Data Sources

- **Primary SQL Dataset**: TravelTide database  
  `test@ep-noisy-flower-846766.us-east-2.aws.neon.tech:5432/TravelTide`
- **CSV Exports**:
  - [Raw CSV from SQL](data/tide_trevel_query_results_all.csv)  
  - [Clustered CSV Output](data/clustering_results_tide_trevel.csv)
---

## 🔍 Methodology

### 🧮 SQL Aggregations
 -[SQL Final view](SQL/SQL_final_view)
- `user_session_agg`: Sessions, bookings, activity labels  
- `user_bags`: Travel intensity via checked bags  
- `user_nights`: Spending, discounts, nights stayed  
- **Final view**: Complete behavior + demographics

📌 Goal: Clean, complete user profile for clustering.

---

## 📊 Feature Overview (23 total)

| Category        | Features                                                                 |
|----------------|--------------------------------------------------------------------------|
| Demographics    | Age, Married, Has Children                                               |
| Activity        | Total Sessions, Avg Clicks, Total Session Time, Avg Duration            |
| Bookings        | Flights, Hotels, Total Cancellations, Checked Bags, Nights              |
| Spending        | Hotel Spend, Flight Spend, Total Spend, Spend per Session               |
| Discount Behavior | Discount Amounts, Discount Ratio, Sensitivity                       |
| Derived         | Booking Ratio, Avg Nights per Booking                                   |

---

## 📈 Clustering Results

### ✅ Preferred Model: `K-Means`
- Chosen over DBSCAN for clearer clusters
- Outliers removed (IQR method)
- Features normalized (log & quantile scaling)

---

## 🧩 Cluster Profiles & Marketing Offers

### 🔵 Cluster 0 – Moderate Travelers
- ~31 sessions, ~16 bookings, ~$17.7k spend  
- 36% have children, moderate discount usage  
🎯 **Offer**: Free Checked Bag – boosts satisfaction

---

### 🟢 Cluster 1 – Heavy Spenders & Frequent Flyers
- ~81 sessions, ~64 bookings, ~$65k spend  
- Long sessions, loyal, low discount usage  
🎯 **Offer**: 1-Night Free Hotel – loyalty reward

---

### 🟡 Cluster 2 – Light Users & Budget-Conscious
- ~21 sessions, ~9 bookings, ~$7k spend  
- 37% have children, highly price-sensitive  
🎯 **Offer**: Exclusive Discounts / No Cancellation Fees

---

## 📊 Additional Offer Mapping

| Offer                | Target Cluster | Justification                              |
|----------------------|----------------|--------------------------------------------|
| Free Hotel Meal      | Cluster 0      | Moderate travelers staying in hotels       |
| Free Checked Bag     | Cluster 0      | Families with moderate travel frequency    |
| No Cancellation Fees | Cluster 2      | Risk-averse, low confidence users          |
| Exclusive Discounts  | Cluster 2      | Highly price-sensitive                     |
| 1-Night Free Hotel   | Cluster 1      | Premium users, loyalty reinforcement       |

---

## 📌 Summary Insights

- **Cluster 1**: Highest LTV → reward and retain
- **Cluster 0**: Mid-tier → encourage more engagement
- **Cluster 2**: Low spenders → activate with offers

---

## 🔄 Future Improvements

- **Interactive Dashboard**: Build with Streamlit or Tableau
- **Recommender System**: Suggest optimal offer per user
- **Scheduled Updates (Airflow)**:
  - Pull fresh SQL data
  - Monthly re-clustering
  - Push to CRM/dashboard

---

## 🧪 Testing & Validation

- **Silhouette Score**: `0.29` → clusters are distinct enough
- **Outlier removal**: IQR-based
- **Normalization**: log and quantile scaling
- **Manual validation**: clusters match marketing logic

---

## 📘 How to Run the Project

### 📦 Requirements

```bash
pip install pandas numpy scikit-learn seaborn matplotlib jupyter
```

---

### 🧪 Steps

1. **Extract Data**: Use SQL to export data to CSV
2. **Load in Python**:
```python
import pandas as pd
df = pd.read_csv('customer_data.csv')
```
3. **Preprocess & Cluster**:
```python
# Normalize, fit KMeans
# Assign cluster labels
```
4. **Visualize**:
```python
import seaborn as sns
sns.boxplot(data=df, x='cluster', y='total_spent')
```
5. **Export**:
```python
df.to_csv('clustering_results_tide_travel.csv', index=False)
```

---

## 🧭 Folder Overview

```
├── SQL/                    # SQL scripts and queries
├── data/                   # Raw and processed CSV files
├── notebooks/              # Jupyter Notebooks (EDA + Clustering)
├── report_and_presentation/ # Reports and slides for marketing
└── README.md
```

---

## 👩‍💻 Author

**Marianna Gokova**  
*Data Analyst*  
📎 [LinkedIn](https://www.linkedin.com/in/marianna-kravchenko)  
📅 *Date: 21.04.2025*
