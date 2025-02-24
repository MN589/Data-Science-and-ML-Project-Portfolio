## Problem Statement: 
This project aims to segment customers for a global e-commerce business to improve marketing 
efforts. Using data ((SAS, 2024)) from 47 countries over five years, we’ll group customers based 
on features such as age, purchase frequency, recency, customer lifetime value (CLV), and 
average unit cost. These clusters will help the company better understand customer behavior, 
target specific groups more effectively, retain loyal customers, and identify opportunities for 
growth.

## Method 
### Data Exploration 
The dataset consists of 951,668 rows representing orders placed on an e-commerce website 
between January 1, 2012, and December 30, 2016. It includes customer features such as Total 
Revenue, Unit Cost, Customer ID, Order ID, Order Date, Delivery Date, Quantity, etc: 
During the data exploration phase, several issues were identified: 
• Duplicate Rows 
• Missing Values 

### Data Cleaning and Feature Engineering 
After data quality assessment, irrelevant features were removed to focus on those that directly 
support customer segmentation: Frequency, Recency, Customer Lifetime Value (CLV), 
Average Unit Cost, and Customer Age.  
New features were created, and duplicate rows were removed. To identify outliers, the Isolation 
Forest method was used with a contamination parameter of 5%. The identified outliers were 
removed.

### Data Aggregation and Clustering 
 
To segment the data, orders were grouped by Customer ID. The following aggregation was 
performed: 
• Sum of CLV per customer. 
• Average Frequency per customer. 
• Minimum Recency per customer. 
• Average Unit Cost per customer. 
 
 
### Optimum number of clusters Analysis: 
To segment customers effectively, identifying the optimum number of clusters is essential.The 
optimum number of clusters was determined using three methods: 
 
1. Elbow Method
2. Silhouette Score 
3. Hierarchical Clustering (Dendrogram)

### K-Means Clustering 
K-Means clustering was then applied to segment customers based on the key features (CLV, 
Frequency, Recency, etc)

### Boxplot Analysis: 
We then performed a boxplot analysis to visualize the distribution of key features—Frequency, 
Recency, Average Unit Cost, Age, and Customer Lifetime Value (CLV)—across the four customer 
clusters. 

### 2-D Visualisation’s using PCA and t-SNE 
We carried out 2D visualizations using PCA and t-SNE to assess separations between customer 
groups.

## Conclusion
From the boxplot analysis and t-SNE, please note the following:
- Cluster 1 has the highest median frequency, indicating frequent, engaged customers. In 
contrast, Cluster 3 shows the lowest frequency, suggesting less frequent buyers. Clusters 
0 and 2 exhibit similar frequency and recency, sitting between Cluster 1 and Cluster 3 in 
terms of engagement. 
- In terms of recency, Cluster 1 has the lowest median, signalling recent purchases and high 
engagement, while Cluster 3 has the highest recency, indicating a longer gap since the last 
purchase, which may signal a risk of churn. Clusters 0 and 2 lie in the middle. 
- For Avg_Unit_Cost, Clusters 0, 1, and 2 have similar median values, indicating comparable 
spending behaviors. Cluster 3 has a slightly lower median but greater variability, 
suggesting diverse purchasing behaviors within the group. 
- In terms of age, Cluster 3 shows the highest IQR, indicating a broader age range, with both 
younger and older customers. Cluster 2 has the highest median age, suggesting older 
customers. Its lowest age is higher than that of Clusters 0 and 1. Clusters 0 and 1, with 
median ages under 50, are predominantly younger, likely more engaged in frequent, lower
cost purchases. Clusters 2 and 3, with median ages over 50, likely consist of older 
customers, requiring tailored marketing strategies. 
- Based on t-SNE results, we can assume that Clusters 1 and 3 are the distinct purple and 
blue clusters, while Clusters 0 and 2 represent the red and green points that overlap.

## Evaluation
- It would have been more appropriate to use 3 as the number of clusters. This is because in 
the visualizations, particularly from t-SNE and PCA, there is significant overlap between the 
green and red clusters, which suggests that these groups might share similar 
characteristics.

## Reference
SAS, 2024. CUSTOMERS_CLEAN [Data set]. SAS. Last revised on 15 December 2021. 
[Accessed 20 February 2024]. 
