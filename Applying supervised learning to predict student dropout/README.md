# Applying supervised learning to predict student dropout

Problem Statement: Confidential_Client plans to develop a predictive model that identifies at-risk adult learners early, enabling targeted interventions that improve retention.

In this project, we will examine student data and use supervised learning techniques to predict whether a student will drop out. In the education sector, retaining students is vital for the institution's financial stability and for students’ academic success and personal development. A high dropout rate can lead to significant revenue loss, diminished institutional reputation, and lower overall student satisfaction.

The three Datasets provided are:

1.  Applicant and course information
2.  Student and engagement data
3.  Academic performance data

These stages reflect Confidential_clients real-world data journey and how student information has progressed and become available.This approach will assist in determining at which stage of the student journey interventions would be most effective.

## Method

### Data Cleaning 
During this analysis, features with high cardinality (more than 200 unique values) and those with a 
high percentage of missing values (50% or more) were dropped in each Stage Dataset.

### Feature Engineering 
A new feature, Age, was derived from Date of Birth, highly correlated features were merged to 
reduce dimensionality and address multicollinearity—Centre Name and Progression University 
were combined into Centre_University, while Booking Type and Lead Source were merged into 
Booking_LeadSource. Categorical variables were encoded using One-Hot Encoding for nominal 
features and Ordinal Encoding for ordinal features 
In the stage 2 and 3 Dataset the additional features (not in Stage 1) were all numeric but contained 
missing values. These missing values were imputed using median for the features with skewed 
distribution, mode for features with extremely skewed distribution. 

### Target Variable Definition: 
The target variable defined for our model was ‘Completed Course’. 
Before splitting the data the target variable ‘CompletedCourse’ was analysed for imbalance. Upon 
evaluating the distribution of the target variable, it was found the target variable was imbalanced. 
Approximately 85% of the target values were in the Completed Course class, while the remaining 
15% represented students who did not complete the course.

### Features Used for Training the Model at Each Dataset Stage: 
Stage 1: 
o The model was trained using the following features: Course Level, Completed 
Course, Is First Intake, Age, Gender, Nationality, Course Name, Centre_University, 
and Booking_LeadSource. 
Stage 2: 
o All Stage 1 features were used, with Authorised Absence added. 
Stage 3: 
o The model was trained using all features from Stage 2, along with Assessed 
Module, Passed Module, and Failed Module. 
- The features used to train the model and test were 80-20 split.

### Neural Network Modelling Approach: 
The sequential model type was used to build our neural network model, this is because we used 
one input data set and want one output and used no branches in our model.  
In our initial model we used the following hyperparameters: 
- Binary cross-entropy loss function was used as this is a binary classification 
- Relu was the chosen hiddenlayer activation function, sigmoid activation function was used 
in the output layer 
- 2 hidden layers was chosen since the data set has only 25059 rows 
- 128 neurons was used in the first hidden layer and in the second hidden layer the number 
of neurons was halved 
- 1 neuron was used in the output layer 
- Adam Optimiser was selected as the initial optimiser for this model 
- L1 regulariser with 0.001 alpha strength was selected in the initial model to prevent 
overfitting as it is better at dealing with sparse one-hot encoded features. 
- The metrics, Accuracy, Precision, Recall, AUC were recorded for our model when it was 
ran for 20 epochs with a batch size of 32.

Stage 1 Dataset Model Training: 
- The initial model was then trained on the training dataset, and the loss curve was plotted to 
assess convergence. 
- The model was then evaluated on the test dataset, and the performance metrics (Accuracy, 
Precision, Recall, and AUC) were calculated. 
- Hyperparameter tuning was then conducted on the following parameter ranges:  
o Neurons: [32, 64, 128] 
o Activations: ['relu', 'tanh'] 
o Regularization: [L1 regularization with 0.001, L1 regularization with 0.01] 
o Optimizers: ['adam', 'rmsprop'] 
o The architecture (number of hidden layers), epochs (20), and batch size (32) were 
kept constant during tuning. 
o The combination of hyperparameters that achieved the highest validation AUC score 
was selected, as AUC is a robust metric for evaluating performance on imbalanced 
datasets. 
- The best combination of hyperparameters from the tuning phase was used to train the final 
model.
- Performance metrics were recorded and evaluated.

Stage 2 & Stage 3 Dataset Model Training:
- The initial models and hyperparameters from previous stages were used as starting points 
for training and testing Stage 2 and Stage 3 Datasets. 
- Hyperparameter tuning was conducted similarly, and the best combination (based on the 
highest validation AUC) was selected to build the final model. 
- Performance metrics were recorded for the initial & final models for the models. 

### XGBoost Modelling Approach: 

Stage 1 Dataset Model Training 
- The initial model was run with default hyperparameters to establish a baseline. 
Performance metrics (accuracy, AUC, precision, and recall) were recorded. 
- A feature importance chart was generated using the training data to identify key features. 
Hyperparameter Tuning: 
o A grid search was conducted to find the best combination of hyperparameters based 
on the highest AUC score. The following hyperparameters were tuned: 
o alpha: [0.1, 0.3, 0.5] 
o max_depth: [3, 5, 7] 
o learning_rate: [0.01, 0.1, 0.2] 
o n_estimators: [50, 100, 200] 
• Final Model: 
o The best hyperparameter combination was used to train the final model, and 
performance metrics were recorded.

Stage 2 and Stage 3 Training 
• The initial models and hyperparameters from previous stages were used as starting points 
for training and testing the Stage 2 and Stage 3 models respectively. 
• Hyperparameter tuning was conducted for both stages, with the best combinations selected 
based on the highest validation AUC. 
• Performance metrics were recorded for both the initial and final models in each stage. 

## Results
### Neural Network Model Results
- please see the notebook 'Confidential_Company_Supervised_Learning_Project.ipynb'
### XGBoost Model Results
- please see the notebook 'Confidential_Company_Supervised_Learning_Project.ipynb'
  
## Conclusions:

-	Both the XGBoost and Neural Network models demonstrate that the most significant improvement in performance metrics comes from the quality and relevance of features rather than hyperparameter tuning. This is evident from the substantial increase in performance metrics between Stages 2 and 3, compared to the minimal or no improvement observed between the final model in Stage 1 and the initial model in Stage 2.
-	The hyperparameter tuning in each stage showed small improvement in the performance metrics in both XGBoost model and the neural networks.
-	XGBoost scored higher than the neural network model in the accuracy and AUC in all three stage datasets, with neural network model scoring slightly higher on precision in only stage 3.
-	XGBoost models were a lot faster to use and created interpretability with the feature importance chart it provided. This allowed for identifying key features
-	The models show that stage 2 model prediction is not greatly better than stage 1 and significantly lower than stage 3. The feature importance chart  emphasises this as all of the top 10 features come from either stage 1 or 3 dataset.

## Evaluation
-	Due to computing restrictions, hyperparameters were tuned in a limited range, this means we may not have fully captured the best hyperparameters for this model
-	The reliability of our model can be improved by increasing the number of epochs
-	The dataset especially for stage 1 consisted of mostly categorical data, this reduced the interpretability of our model’s decision-making process
-	The importance of stage 2 may have been reduced due to unauthorised absence being removed for high cardinality.
