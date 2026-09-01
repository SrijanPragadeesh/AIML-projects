# Online Education Dataset Analysis

## 📌 Project Overview

This project analyzes an **Online Education Dataset** to understand how student engagement affects their academic performance.

## 📊 Analysis Performed

* Checked student `final_result` distribution.
* Calculated pass rate based on `engagement_level`.
* Handled missing values in `total_clicks` and `pass_flag`.
* Created a visualization of pass rate by engagement level.
* Applied **StandardScaler** for feature scaling.
* Built a **Logistic Regression** model using `total_clicks` to predict `pass_flag`.

## 🛠️ Technologies Used

* Python
* Pandas
* NumPy
* Seaborn
* Matplotlib
* Scikit-learn

## 📁 Project Structure

```text
Online-Education-ML/
├── Dataset/
│   └── online_education_dataset.csv
├── Notebook/
│   └── online_education.ipynb
├── Output/
│   └── pass_rate_by_engagement.png
└── README.md
```

## 🎯 Objective

To analyze student engagement and build a simple machine learning model to predict whether a student will pass.

## 📈 Visualization

The project includes a bar chart showing the **Pass Rate by Engagement Level**.
