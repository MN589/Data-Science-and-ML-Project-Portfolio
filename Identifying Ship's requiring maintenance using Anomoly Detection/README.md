# Project: Detecting the anomalous activity of a ship’s engine

## **Business context**
You are provided with a real data set to identify anomalous activity in a ship’s engine functionality (Devabrat,  2022). As you work through this project, keep in mind that, typically speaking, anomalies would make up a minority of the data points (i.e., about 1% to 5% of the data points would be anomalies).

The data set contains six important features continuously monitored to evaluate the engine's status as ‘good’ or ‘bad’. These features are:
- **Engine rpm (revolutions per minute):** A high rpm indicates the engine is operating at a higher speed than designed for prolonged periods, which can lead to overheating, excessive wear, and eventual failure. A low rpm could signal a lack of power, issues with fuel delivery, or internal mechanical problems.
- **Lubrication oil pressure:** Low lubrication oil pressure indicates insufficient lubrication, leading to increased friction, overheating, and engine damage. A high lubrication oil pressure could signal a blockage in the oil delivery system, potentially causing seal or gasket failure.
- **Fuel pressure:** High fuel pressure can cause poor engine performance and incomplete combustion, indicating fuel pump or filter issues. A low fuel pressure may result in excessive fuel consumption, poor emissions, or damage to the fuel injectors.
- **Coolant pressure:** Low coolant pressure indicates a potential leak in the cooling system or a coolant pump failure, risking engine overheating. A high coolant pressure could be a sign of a blockage in the cooling system or a failing head gasket, which can also lead to overheating.
- **Lubrication oil temperature:** High lubrication oil temperature suggests the oil is overheating, which can degrade its lubricating properties and lead to engine damage. A low lubrication oil temperature may indicate it is not reaching its optimal operating temperature, potentially causing inadequate lubrication.
- **Coolant temperature:** High coolant temperature signals overheating, which various issues, including a failed thermostat, coolant leak, or insufficient coolant flow can cause. A low coolant temperature could suggest the engine is not reaching its optimal operating temperature, affecting performance and efficiency.

Issues with engines could lead to engine malfunctions, potential safety hazards, and downtime (e.g. delayed deliveries), resulting in the breakdown of a ship’s overall functionality, consequently impacting the business, such as affecting revenue via failure to deliver goods. By predicting timely maintenance, the business aims to increase profit by reducing downtime, reducing safety risks for the crew, limiting fuel consumption, and increasing customer satisfaction through timely deliveries.

Your task is to develop a robust anomaly detection system to protect a company’s shipping fleet by evaluating engine functionality. Therefore, you’ll explore the data and:
- employ preprocessing and feature engineering
- perform model training, anomaly detection, post-processing, and refinement.

You must prepare a report illustrating your insights to the prospective stakeholders, showing how your solution will save the business money and build trust with its stakeholders. At this stage of the project, the main question you need to consider is:
- What insights can be gained from the data, and what recommendations can be made to the company based on these insights? For example, which features need to be monitored closely, and what are the thresholds for anomalous observations? Which statistical or ML technique is the best for anomaly detection based on **this data set**, and which feature (univariate approach) or combination of features (multivariate approach) can predict maintenance ?

# Methodology
We utilised three different approaches to identify ships with anomolous activity within the threshold established

## Statistical Approach 1 - IQR Method
To identify anomalies within such data, the Interquartile Range (IQR) method was applied to each of the six individual columns.

1) Calculated the IQR for each feature, (IQR= Q3-Q1)

2) Anomaly threshold established - any data value below Q1-1.5(IQR) or above Q3+1.5(IQR)

3) All data values in each feature is checked and flagged if its an anomaly.

4) The sum of anomalies for each ship is calculated.

Based on previous studies, approximately 1-5% of ships are expected to display anomalous engine functionality. To align with this expectation, we calculated the percentage of ships exhibiting anomalies across one, two, three, or four features.

### Conclusion from utilising Statistical Approach 1
- The majority of ships (21.6%) exhibited anomalies in a single feature, which is insufficient to justify maintenance intervention. It would be costly and not feasible to use this condition to identify ships requiring servicing and maintenance.
- Ships with anomalies in three or more features were exceedingly rare (<0.1%), and no ships had anomalies in all four features.Ships with anomalies in two features should be flagged for further investigation and potential maintenance.
- Using the 1-5% magnitude provided to us by the client, we determined that any ship engine with 2 or more outliers detected will be flagged. Ships with 2 or more outliers detected provide anomolus activity of 1-5%.

## ML Approach 1 - Machine Learning using One-Class SVM Method

1) The data was first scaled using standardisation

2) A range of gamma and nu values were tested to identify the parameter combination thatbest aligns with the expected 1-5% anomaly rate.

3) We sum the number of ships with anomalies and calculate the percentage of ships overall that have anomalous engine functionality.

The following Combination of Parameters were used:
1. Gamma = auto and NU= 0.2
2. Gamma = auto and NU=0.05
3. Gamma = auto and NU = 0.02
4. NU = 0.02 amd Gamma = 0.2
5. NU = 0.02 and Gamma = 0.1
6. NU= 0.02 and Gamma = 0.05

### Conclusion from utilising Machine Learning using One-Class SVM Method
- With lower nu values (like 0.02), the model becomes stricter, potentially
resulting in false negatives, where some anomalies go undetected
- The choice of nu = 0.05 when keeping gamma is 0.167 balances the need to detect engine issues while minimising unnecessary maintenance checks. It results in a 5% anomaly detection rate, aligning with the desired threshold.
- From the PCA visualisations, most of normal points are clustered tightly in the centre, which indicates that most ship engine data falls within normal range,
- There are red anomalies that are inside the blue clustered centre which suggest there are subtly issues that are not immediately obvious but need further investigation. It could be noise or an early indicator of engine performance issues
- Most of the anomalies form a ring around the blue normal data. This suggest that most anomalies are mild deviations, these data points could represent an early stage issue that warrants further monitoring.
- Few data points deviate significantly from the normal cluster and represent strong outliers, these ships may require immediate investigation

## ML Approach 2 – Anomaly detection with Isolation Forest ML model
1) No Scaling was required for this algorithm

2) In Isolation Forest, the contamination parameter directly sets the percentage of anomalies, making it simple to control detection rates.

3) Contamination parameter was set to 5% as it ensures that more anomalies are detected within our 1-5% desired detection rate.

4) The n_ estimators parameter was set to 100 as it is a good balance between model stability and computational efficiency.

### Conclusion from utilising Machine Learning using Isolation Forest Method
- In Isolation Forest, the contamination parameter directly sets the percentage of anomalies, making it simple to control detection rates

## Evaluation 
Review of Approaches:
- The dataset contains 19,534 rows, which is relatively small for machine learning, and has low correlation between features, making anomaly detection challenging using the IQR method. Machine learning methods are more practical for this type of data as they can account for feature interactions, unlike IQR, which analyzes features independently and is less suitable for multivariate anomaly detection.

- One-Class SVM is better suited than the other two in capturing anomalies in higher-dimensional space.

- Given the scenario, machine learning methods are more practical, as IQR is designed to analyze each feature independently, making it less effective for detecting anomalies arising from interactions between multiple features. Machine learning models, on the other hand,can account for relationships between features.
