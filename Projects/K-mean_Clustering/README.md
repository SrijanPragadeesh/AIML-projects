# Large-Scale Geographic Consumer Clustering & High-Dimensional Visualizations

## Mini Project

### Student Project

This project demonstrates how Machine Learning can be used to group similar real-estate locations into different clusters using the **K-Means Clustering** algorithm.

Although the project title sounds advanced, the implementation is kept simple so that beginners can understand every step.

---

## Project Objective

The objective of this project is to:

- Load a real-estate/property dataset
- Clean the dataset
- Select numerical features automatically
- Scale the data
- Apply K-Means Clustering
- Visualize the clusters
- Analyze the characteristics of each cluster
- Predict the cluster for a new property sample

This project helps identify similar housing markets that could support business expansion and customer segmentation.

---

## Machine Learning Algorithm

**Algorithm Used:** K-Means Clustering

K-Means is an unsupervised machine learning algorithm.

It groups similar data points together based on their numerical features.

---

## Libraries Used

- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn

No advanced AI techniques are used.

---

## Dataset

The project uses a CSV file containing property information.

Example columns include:

- Property_ID
- Latitude
- Longitude
- Property_Area_sqft
- Bedrooms
- Bathrooms
- Age_of_Property
- Parking_Spaces
- Nearby_Schools_km
- Nearby_Hospitals_km
- Crime_Index
- Population_Density
- Average_Income
- Property_Price
- Property_Type
- City

The notebook automatically detects numerical columns and adjusts if column names are different.

---

## Project Workflow

### Step 1
Import required libraries.

### Step 2
Upload and load the dataset.

### Step 3
Display the first five rows.

### Step 4
View dataset information.

### Step 5
Check for missing values.

### Step 6
Automatically select numerical columns.

### Step 7
Clean missing values.

### Step 8
Scale the features using StandardScaler.

### Step 9
Use the Elbow Method to find the best number of clusters.

### Step 10
Train the K-Means model.

### Step 11
Assign cluster labels to each property.

### Step 12
Visualize the clusters using a scatter plot.

### Step 13
Display the average values of each cluster.

### Step 14
Predict the cluster for a new sample.

### Step 15
Summarize the results.

---

## Output

The notebook produces:

- Cleaned dataset
- Elbow Method graph
- Clustered dataset
- Scatter plot of clusters
- Cluster summary table
- Cluster prediction for a new property

---

## Applications

This project can be used in:

- Real Estate Analysis
- Customer Segmentation
- Housing Market Analysis
- Urban Planning
- Business Expansion Planning
- Property Investment Analysis

---

## Folder Structure

```
Project Folder
│
├── K-mean_Clustering.ipynb
├── Large_Scale_Geographic_Consumer_Clustering_Dataset_100000_Rows.csv
└──  README.md
```

## Conclusion

This beginner-friendly project demonstrates how K-Means Clustering can group similar real-estate locations into meaningful clusters.

The project covers the complete machine learning workflow, including data loading, preprocessing, feature scaling, clustering, visualization, and prediction, making it suitable for first-year and second-year AI/ML students.

---

## Author

**Name:** Srijan Pragadeesh

**Course:** Bachelor of Computer Applications (BCA)

**Project:** Mini Project – AI/ML
