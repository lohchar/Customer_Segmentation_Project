# Customer Segmentation Project
## Overview
- This project applies unsupervised machine learning techniques to segment customers based on purchasing behavior. The main goal is to discover meaningful groups (clusters) of customers using methods like K-Means, Hierarchical Clustering, PCA, and t-SNE.
## Part A — Load & basic EDA
- Imported libraries and loaded both datasets (Online retail & Mall customers) 
- Renamed column to Gender in mall customers dataset
- The online retail dataset has 541909 rows and 8 columns. Showed the column names and theirs data types.
- Showed unique values per column in online retail dataset where InvoiceNo has the most 25900 while lowest is country with 38. Showed the most frequent values in country column. United Kingdom had the most 495478.
- For the mall customers dataset, customerID had the most unique values, 200 while lowest was gender with 2. Female category had the most frequent values in the gender column with 112 and male 88
- CustomerID had the most missing values, 135080 and Description 1454 in the online retail dataset
- showed the summary statistics;mean, median, std, min, max, quartiles for numeric columns
- Converted Age to Young, Adult and Senior bins where Adult had the highest count, 120.
- Identified 2517 unrealistic values
- Identified 4372 uniques customers and Adult as the most common group 
## Part B — Data cleaning & filtering
- Droped rows with missing values in CustomerID
- Dropped 5225 duplicate rows from the online retail dataset
- Filtered out records in mall customers dataset where age is less that 18
- Created a new category, PriceCategory, in retail dataset using conditional statements
- Confirmed all numeric columns in Mall customers dataset have no missing values to be replaced with mean 
- Used quantiles to bucket customers in to categories in SpendingLevel column
- Applied feature scalling to numeric columns(Quantity and UnitPrice)
## Part C — Aggregation & feature engineering
- Computed average income by gender using groupby, Male-62.227273 and Female-59.250000
- Calculated and showed max, min, and mean for numeric columns per group
- Created a new ratio feature, Income_to_Age column.
- Flagged “High value” customers based on income and spending greater than average.
- CustomerID & Annual income show a very strong positive correlation, 0.97. It suggests that in the dataset, CustomerID is ordered in a way that increases with income (possibly synthetic data where IDs were assigned in order). Strong negative correlation is shown by Age and Income_to_Age columns suggesting lower income/age ration for older customers
- Identified female as the gender with the higher average spending score
- Created a pivot table by age group and gender for average spending.Young females had the highest average spending while senior male had the lowest
## Part D — Visualizations & group exploration 
- Visualized age distribution using a histogram where most customers were around 30-40 years
- Visualized average spending by gender where the bar chart indicates female had the highest average spending score compared to male gender.
- Visualized Annual Income and spending score using a scatterplot which showed the different groups of customers(high spending, low spending etc). It is clear there is high variance in spending across income levels whereby income does not perfectly predict spending behaviour
- Visualized spending score by age groups using a boxplot. It indicates young customers had the highest median spending compared to adult and senior. Senior customers were more clustered in the low level spending compared to high level 
- Visualized the correlation between numeric features using a heatmap. Strong negative correlation was shown between columns like age & income_to_age while strong negative was shown by age & income_to_age
## Part E — Dimensionality reduction (PCA & t-SNE)
- Visualized explained variance using a barplot after running PCA on standardized income and spending features.It is clear that both PC1 & PC2 explain an almost equal percentage of the total variance.This means both income and spending features are equally  important in capturing customer behaviour
- Visualized 2D PCA components scatter colored by gender. It is clear there is no distinct separation or clear boundary between the male and female data points. The two groups are heavily intermingled.It suggest that income and spending features captured by PC1 & PC2 are not predictors of gender 
- Run t-SNE and plot the 2D embedding using a scatterplot. The plot shows several distinct clusters of data points, confirming the algorithm has successfully separated the customers into different groups.Each cluster represents a group of customers who are similar to each other in terms of their income and spending habits.
- PCA plot shows customers arranged along axes that reflect income & spending variation. You’ll see some spread but clusters won’t be very distinct.   
- t-SNE plot typically reveals more distinct, blob-like clusters, often aligning with customer segments (e.g., high spenders vs. low-income groups).   
- t-SNE shows clearer clusters, but PCA is easier to interpret and reproducible.
## Part F — Clustering & evaluation
- Ran k-means for k=2…10 on standardized features and visualized using the elbow curve.The plot indicates the inertia drops sharply from k=2 to k=5.At k=5, the curve makes a distinct bend, resembling an elbow.After k=5, the curve becomes much flatter making the optimal no. of cllusters to be 5. While the inertia continues to decrease, the improvement is minimal. Adding more clusters beyond this point doesn't offer much benefit and can lead to overfitting.
- Computed silhouette score for each k and identified k=5 as the best k.Its because this value of k has the highest silhoutte score, which indicates best separation between clusters. 
- Visualised the chosen K =5 using a scatter plot. It indicates the algorithm has successfully partitioned the data into five distinct groups, each represented by a different color and a centroid marked with a black 'X'.
- Visualized a dendogram after running hierarchical clustering. It shows how data points are merged into clusters based on their similarity. The vertical axis represents the distance or dissimilarity between clusters, while the horizontal axis represents the individual data points (customers).
- The comparison table and dendrogram show that both K-Means and Hierarchical Clustering have found similar underlying cluster structures in the data. The K-Means algorithm and the Hierarchical algorithm have largely identified the same customer segments, which reinforces the validity of the discovered clusters
- Profiled each cluster to shows the average characteristics for each of the five K-Means clusters. Cluster 0 is the largest segment, containing more than double the number of customers in any other cluster, while Cluster 2 is the smallest. This suggests that the "average" customer profile which corresponds to Cluster 0 is the most common type in mall customers dataset.
- The cluster assignments did change with different random states. The output you provided shows the labels for the same data points shifting between runs. For example, a data point that was assigned to cluster 0 in one run might be assigned to cluster 4 in another run.
- Exported the dataset with cluster labels to csv
