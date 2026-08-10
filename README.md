# 🚚 Porter Delivery Analytics | Python

## 📊 Project Overview

This project performs an end-to-end **Exploratory Data Analysis (EDA)** of Porter food-delivery order data using Python.

The analysis focuses on understanding **delivery performance, order patterns, market-level behavior, store categories, order value, delivery partners, and operational factors** that may influence delivery duration.

The project includes data cleaning, feature engineering, statistical analysis, correlation analysis, outlier detection, and interactive data visualization.

<img width="1023" height="532" alt="image" src="https://github.com/user-attachments/assets/b1bc17ab-0898-4bd1-a2c3-9e93aad55002" />


---

## 🎯 Business Objective

The primary objective of this project is to analyze delivery operations and answer questions such as:

- How long do orders typically take to be delivered?
- Which markets generate the highest order volumes?
- Which food categories have the longest delivery times?
- What time of day has the highest order activity?
- Which days generate the most orders?
- What is the average order value?
- How does the number of items affect order value?
- How does the number of delivery partners relate to delivery time?
- Which order protocols are more efficient?
- Which markets have higher average order values?
- What proportion of orders are delivered within 30 minutes?
- Which categories contribute the most high-value orders?
- Which markets show the highest variability in delivery time?
- How does partner availability differ across markets?

---

# 📂 Dataset

The dataset contains **197,428 orders** and **14 original columns**.

### Key Variables

| Column | Description |
|---|---|
| `market_id` | Market identifier |
| `created_at` | Order creation timestamp |
| `actual_delivery_time` | Actual delivery timestamp |
| `store_id` | Store identifier |
| `store_primary_category` | Primary store/food category |
| `order_protocol` | Ordering protocol |
| `total_items` | Total number of items |
| `subtotal` | Order subtotal |
| `num_distinct_items` | Number of distinct items |
| `min_item_price` | Minimum item price |
| `max_item_price` | Maximum item price |
| `total_onshift_partners` | Delivery partners currently on shift |
| `total_busy_partners` | Busy delivery partners |
| `total_outstanding_orders` | Outstanding orders |

---

# 🧹 Data Cleaning & Preparation

## 1. Date Conversion

The following columns were converted from object/string format to datetime:

- `created_at`
- `actual_delivery_time`

This enabled time-based calculations and analysis.

---

## 2. Delivery Duration

A new feature called:

`delivery_duration`

was created by calculating the difference between:

`actual_delivery_time - created_at`

The duration was then converted into minutes as:

`delivery_duration_minutes`

---

## 3. Missing Value Analysis

Missing values were identified across the dataset.

The highest missing-value percentage was observed in:

- `total_onshift_partners`
- `total_busy_partners`
- `total_outstanding_orders`

with approximately **8.24%** missing values.

Other columns with missing values included:

- `store_primary_category`
- `order_protocol`
- `market_id`
- `actual_delivery_time`

---

## 4. Missing Value Treatment

The project handled missing values using different approaches:

### Dropped

Rows with missing delivery duration were removed.

**7 rows** were removed, leaving:

**197,421 orders**

### Mode Imputation

The following variables were filled using their mode:

- `market_id` → 2
- `order_protocol` → 1
- `store_primary_category` → american

### Median Imputation

The following operational variables were filled using their median:

- `total_onshift_partners` → 37
- `total_busy_partners` → 34
- `total_outstanding_orders` → 41

After imputation, no missing values remained.

---

# ⚙️ Feature Engineering

Several new analytical features were created.

### Time Features

From `created_at`:

- `order_day_of_week`
- `order_hour_of_day`

From `actual_delivery_time`:

- `delivery_day_of_week`
- `delivery_hour_of_day`

### Partner Availability

A new variable was created:

`available_partners`

calculated as:

```text
total_onshift_partners - total_busy_partners
