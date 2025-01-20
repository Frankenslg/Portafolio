# Data Analyst

## Projects
### Project 1:
# 🚀 **Optimizing Carsharing Rates: A Dynamic Web Application**

## 🌐 **Interactive Data Exploration with Streamlit**

This project involves the development of an interactive web application using Streamlit, designed to empower users with visual data exploration of car sales advertisements.

---

## 🛠️ **Step 1: Getting Started**

### 🔧 **Laying the Foundation**
- **GitHub and Render.com Accounts:** Set up accounts on these platforms to host the project repository and streamline app deployment.
- **Environment Configuration:** Establish a virtual environment, `vehicles_env`, to manage dependencies like pandas, streamlit, and plotly-express—essential for data analysis and app development.
- **Tools in Action:** Use Visual Studio Code for seamless coding and git repository management.

---

## 📥 **Step 2: Data Acquisition**

### 🗂️ **Harnessing the Dataset**
- **Data Download:** Download and place the `vehicles_us.csv` dataset in the project directory. This will serve as the foundation for exploratory data analysis (EDA) and visualizations in the web app.

---

## 🔍 **Step 3: Exploratory Data Analysis**

### 📊 **Insights at a Glance**
- **Jupyter Notebook Setup:** Create a Jupyter Notebook (`EDA.ipynb`) within a dedicated `notebooks` directory for preliminary data exploration.
- **Visualization with Plotly Express:** Utilize histograms and scatter plots to reveal data distributions and correlations, ensuring a solid understanding of the dataset.

---

## 🖥️ **Step 4: Web Application Development**

### 🌟 **Building the Dashboard**
- **Main Application File:** Develop `app.py` at the root of the project directory as the centerpiece of the Streamlit app.
- **Features at a Glance:**
  - **Library Integration:** Import essential libraries for functionality.
  - **Data Loading:** Read and prepare the dataset for visualization.
  - **Interactive Interface:** Craft a user-friendly UI with a main header and interactive buttons, enabling users to generate histograms and scatter plots dynamically.

---

## 🎯 **Project Objective: Simplifying Insights**

The goal is to demonstrate proficiency in Python programming and modern web application development by creating a platform that offers interactive data exploration. This dynamic tool allows users to gain insights through real-time visualizations, paving the way for scalability and adaptation to future datasets or projects.

**Check out the live app:** [Streamlit Dashboard](https://sprint-5-diua.onrender.com) 🌟


### Project 2
# A/B Test Analysis: Online Store Funnel Optimization

---

## 🌟 **Introduction**

This project evaluates the results of an A/B test conducted by an international online store to assess the impact of an improved recommendation system. The main goal was to determine whether the new system increases user conversion by at least 10% in three key stages of the purchase funnel:

- **Product Page:** Visits to the product page.
- **Cart Addition:** Adding products to the shopping cart.
- **Purchase:** Completing a purchase.

Through rigorous analysis and interpretation of data, this study identifies the effectiveness of the recommendation system and provides actionable insights for decision-making.

---

## 📊 **Step 1: Data Exploration and Preparation**

### 1.1 **Data Loading**
The datasets used include information on new users, user events, marketing events, and A/B test participants.

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from statsmodels.stats.proportion import proportions_ztest

# Load datasets
data_files = ['/datasets/ab_project_marketing_events_us.csv',
              '/datasets/final_ab_new_users_upd_us.csv',
              '/datasets/final_ab_events_upd_us.csv',
              '/datasets/final_ab_participants_upd_us.csv']

marketing_events, new_users, events, participants = [pd.read_csv(file) for file in data_files]
```

### 1.2 **Data Cleaning**
- **Datetime Conversion:** Converted date columns to proper datetime format.
- **Missing Values:** Handled missing data by retaining only relevant columns.
- **Duplicates:** Checked and confirmed the absence of duplicate entries.

---

## 🌄 **Step 2: Exploratory Data Analysis**

### 2.1 **User Distribution in the Funnel**
The funnel comprises three stages:

1. **Product Page:** Users visiting the product page.
2. **Cart Addition:** Users adding products to the cart.
3. **Purchase:** Users completing a purchase.

```python
# Count unique users at each stage
page_views_users = events[events['event_name'] == 'product_page']['user_id'].nunique()
cart_additions_users = events[events['event_name'] == 'product_cart']['user_id'].nunique()
purchases_users = events[events['event_name'] == 'purchase']['user_id'].nunique()

# Calculate conversion rates
conversion_to_cart = cart_additions_users / page_views_users
conversion_to_purchase = purchases_users / cart_additions_users
```

| Stage              | Users    | Conversion Rate |
|--------------------|----------|-----------------|
| Product Page       | 38,929   | -               |
| Cart Additions     | 19,284   | 49.54%          |
| Purchases          | 19,568   | 33.18%          |

### 2.2 **Event Distribution by Date**
Analyzed the daily distribution of events to identify anomalies or trends.

```python
# Plot daily event distribution
daily_events = events.groupby(events['event_dt'].dt.date).size()
plt.figure(figsize=(10, 6))
daily_events.plot(kind='line')
plt.title('Daily Event Distribution')
plt.xlabel('Date')
plt.ylabel('Number of Events')
plt.show()
```

---

## 🔧 **Step 3: A/B Test Analysis**

### 3.1 **Group Comparisons**
The A/B test compares two groups:

- **Group A:** Control group with the current recommendation system.
- **Group B:** Experimental group with the new recommendation system.

#### Conversion Rates

| Stage                | Group A | Group B |
|----------------------|---------|---------|
| Conversion to Cart   | 31.47%  | 32.99%  |
| Conversion to Purchase | 33.51%  | 32.50%  |

### 3.2 **Statistical Significance (Z-Test)**
A Z-test was used to evaluate whether the observed differences in conversion rates were statistically significant.

```python
# Conversion to Cart
z_stat, p_value = proportions_ztest([success_a_cart, success_b_cart],
                                     [total_a_page, total_b_page])
print(f'Z-Test for Conversion to Cart: z = {z_stat:.2f}, p-value = {p_value:.5f}')

# Conversion to Purchase
z_stat_purchase, p_value_purchase = proportions_ztest([success_a_purchase, success_b_purchase],
                                                       [total_a_cart, total_b_cart])
print(f'Z-Test for Conversion to Purchase: z = {z_stat_purchase:.2f}, p-value = {p_value_purchase:.5f}')
```

- **Conversion to Cart:** Significant improvement (\(p < 0.05\)).
- **Conversion to Purchase:** No significant difference.

---

## 🌟 **Conclusions and Recommendations**

### Key Insights
1. **Conversion Improvement:** The experimental group showed a statistically significant improvement in conversion to the cart stage.
2. **Purchase Conversion:** No significant improvement was observed in the final purchase stage.
3. **Anomalies:** The presence of users in both groups (441 users) may have introduced bias.

### Recommendations
1. **Optimize the Purchase Stage:** Investigate barriers preventing users from completing purchases.
2. **Refine User Segmentation:** Exclude overlapping users in future tests to improve accuracy.
3. **A/B Test Iteration:** Conduct additional tests to validate findings and refine the recommendation system.

---

**Date: 2025-01-06**

**Francisco SLG**
