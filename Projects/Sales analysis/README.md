# Customer Segmentation using RFM Analysis and K-Means Clustering

This repository contains a Python Jupyter Notebook (`Sales analysis notebook.ipynb`) that performs customer segmentation on a retail sales dataset. By leveraging RFM (Recency, Frequency, Monetary) analysis and K-Means clustering, the project groups customers based on their purchasing behavior to help identify key customer profiles.

## Overview
The analysis processes transactional data to extract meaningful customer metrics, scales the features, and applies unsupervised machine learning to find distinct customer segments. 

Key steps in the workflow include:
*   **Data Cleaning:** Removing missing values, cancelled orders, and invalid quantities/prices.
*   **RFM Feature Engineering:** Calculating Recency (days since last purchase), Frequency (number of purchases), and Monetary (total spend) for each customer.
*   **Data Scaling:** Standardizing the RFM values using `StandardScaler` to ensure even feature weighting.
*   **Optimal Cluster Selection:** Utilizing the Elbow Method to determine the ideal number of clusters.
*   **Model Building:** Applying K-Means clustering (k=2) to segment the customer base.
*   **Evaluation:** Assessing cluster quality using the Silhouette Score and Davies-Bouldin Index[cite: 1].

## Dataset
The project uses an Excel dataset named `sales2.xlsx`[cite: 1]. The required columns for this analysis are:
*   `Invoice`: Invoice number[cite: 1]
*   `Quantity`: Item quantity per transaction[cite: 1]
*   `InvoiceDate`: Date and time of the transaction[cite: 1]
*   `Price`: Unit price of the item[cite: 1]
*   `Customer ID`: Unique identifier for the customer[cite: 1]

## Dependencies
To run this notebook, you will need the following Python libraries installed:
*   `pandas`[cite: 1]
*   `scikit-learn`[cite: 1]
*   `matplotlib`[cite: 1]
*   `openpyxl` (required by pandas to read Excel files)

You can install these via pip:
```bash
pip install pandas scikit-learn matplotlib openpyxl
