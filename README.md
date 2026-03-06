# online-retail-recommendation-system
Product recommendation system built using Python and online retail transaction data.




# Online Retail Recommendation System

## Project Overview

This project implements a basic **product recommendation system for an online retail dataset**.

Recommendation systems are widely used in e-commerce platforms to suggest products that customers may be interested in based on their previous purchases. In this project, an **item-based collaborative filtering approach** is used to recommend products by analyzing historical purchase data.

The system identifies relationships between products that are frequently purchased together and suggests similar products to users.

The project also compares the recommendation system with a simple **popularity-based recommendation baseline**.

---

## Dataset

Dataset used: **Online Retail Dataset**

The dataset contains historical transaction data from an online retail store.

### Dataset Columns

| Column | Description |
|------|-------------|
| InvoiceNo | Unique transaction ID |
| StockCode | Product ID |
| Description | Product name/description |
| Quantity | Number of products purchased |
| InvoiceDate | Date of the transaction |
| UnitPrice | Price per product |
| CustomerID | Unique customer identifier |
| Country | Country where the purchase was made |

### Dataset Size

Original dataset:

- **541,909 rows**

After data cleaning:

- **397,924 rows**
- **4,339 customers**
- **3,665 products**

---

## Technologies Used

- Python  
- Pandas  
- NumPy  
- Matplotlib  
- Scikit-learn  
- SciPy  

---

## Project Workflow

### 1. Data Loading

The dataset is loaded using **Pandas** and the `InvoiceDate` column is converted into datetime format for time-based analysis.

---

### 2. Data Cleaning

Several preprocessing steps were performed to clean the dataset:

- Removed cancelled transactions (InvoiceNo starting with **C**)
- Removed rows where **Quantity ≤ 0**
- Dropped rows with missing **CustomerID**
- Checked and corrected data types

This step ensures the data used for the recommendation model is reliable.

---

### 3. Exploratory Data Analysis (EDA)

Basic exploratory analysis was performed to understand the dataset:

- Top countries by number of purchases
- Most frequently purchased products
- Distribution of transactions

These visualizations helped understand overall purchasing behavior.

---

### 4. Interaction Data Preparation

Customer purchase interactions were aggregated by grouping:

```
(CustomerID, StockCode) → Total Quantity Purchased
```

Example structure:

| CustomerID | StockCode | Quantity |
|------------|-----------|----------|
| 12347 | 16008 | 24 |
| 12347 | 17021 | 36 |

This represents how frequently a customer purchased a particular product.

---

### 5. User-Item Matrix

A **user-item interaction matrix** was created where:

- Rows represent **customers**
- Columns represent **products**
- Values represent **purchase quantity**

Matrix size:

```
4339 users × 3665 items
```

Since most customers purchase only a few items, the matrix is **sparse**.

---

### 6. Item-Based Collaborative Filtering

An **item-item collaborative filtering model** was built using **Nearest Neighbors with cosine similarity**.

Steps used:

1. Transpose the user-item matrix
2. Treat each product as a vector
3. Use cosine similarity to find similar products
4. Recommend products based on similarity scores

This approach allows the system to recommend products similar to those already purchased by the user.

---

### 7. Recommendation Function

A recommendation function was implemented that:

1. Finds products already purchased by a user
2. Identifies similar products using the trained model
3. Removes products already purchased
4. Returns the top recommended items

Example recommendation output:

```
Example user ID: 12346

Purchased:
23166

Recommended items:
23165
22652
22985
21984
21980
```

---

### 8. Popularity-Based Baseline

A simple **popularity-based recommender** was also created.

This model recommends the **most frequently purchased products** across all customers.

Example popular products:

```
23843
23166
84077
22197
85099B
```

This model is useful as a **baseline comparison**.

---

### 9. Model Evaluation

To evaluate the models, a **time-based train-test split** was used:

- Training data → earlier transactions
- Test data → last 90 days of transactions

Evaluation metric used:

**Precision@10**

| Model | Precision@10 |
|------|--------------|
| Popularity baseline | 0.03 |
| Item-item recommender | 0.028 |

Both models performed similarly on this dataset.

---

## Project Structure

```
project-folder
│
├── notebooks
│   └── Retail_Recommendation_System_Project_Final.ipynb
│
├── dataset
│   └── online_retail.xlsx
│
└── README.md
```

---

## Conclusion

This project demonstrates how a **basic recommendation system** can be built using purchase history data.

Key learnings from the project:

- Data preprocessing plays a critical role in recommendation systems
- Sparse matrices are useful when dealing with large user-item datasets
- Item-based collaborative filtering can identify meaningful relationships between products
- Baseline models help in comparing model performance

Although the popularity model performed similarly in this case, collaborative filtering approaches generally scale better for larger recommendation systems.

---

## Future Improvements

Possible improvements for this project:

- Implement **matrix factorization techniques**
- Use **implicit feedback recommendation models**
- Incorporate **product descriptions or metadata**
- Apply **deep learning based recommender systems**
- Improve evaluation with additional metrics

---

## Author

This project was developed as part of my Plasmid Data Science Internship , focused on building a basic recommendation system using retail transaction data.
