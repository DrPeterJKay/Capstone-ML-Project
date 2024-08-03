# PREDICTING STUDENT WHO WITHDRAWAL AT UNIVERISTY, TO IMPROVE NON-CONTINAUTATION RATES.


## NON-TECHNICAL EXPLANATION OF YOUR PROJECT
The purpose of this model is to predict at a given point during the course (nominally 50% through) if a student is likely to withdraw from the course.
Students withdrawing are classed as "non-continuation" students and are reported by the university.
The model uses data from the VLE (Virtual Learning Environment), Student Assessment grades and Student Registration information systems to  make the predictions.
The data used to make the predictions was pre-processed. This was a three step process that included: cleaning the data, creating some new features and combining the three datasets.


## DATA
The data that was used to create, train and optimise the models were an open source dataset providede by the Open University.

The data set can be found here: [Open University Learning Analytics Dataset](https://www.kaggle.com/datasets/thedevastator/open-university-learning-analytics-dataset/)

## MODEL 
In my project I evaluated four Machine Learning models. There are:
- Model 1: Decision Tree
- Model 2: Support Vector Machine
- Model 3: k-Nearest Neighbour
- Model 4: Neural Network

A final Naive model (Model 0) was created to bench mark each of the other models. This was a DUmmyClassifier with stratified strategy.

## HYPERPARAMETER OPTIMSATION
Description of which hyperparameters you have and how you chose to optimise them. 

In all cases I used a grid seach methodolgy to optimise the hyperparameters. This is mainly becuase the optimisiation time for the models was relatively short in duration (longest was approximately 15 minutes).

The hyperparameters optimised for each model were:
- Model 1: Decision Tree.
  - Maximum Tree Depth
- Model 2: Support Vector Machine
  - C parameter
  - gamma parameter
- Model 3: k-Nearest Neighbour
  - Number of nearest neighbours
  - Weights (of neighbours)
- Model 4: Neural Network
  - Number of nodes in the first hidden layer
  - Number of nodes in the second hidden layer


## RESULTS
The table below summarised the results:

| Model 	| F1-score (train) 	| F1-score (val) 	| Optimisation Time 	| Train Time 	| Run Time 	|
|------:	|-----------------:	|---------------:	|------------------:	|-----------:	|---------:	|
| Naive 	|              N/A 	|           0.16 	|               N/A 	|        N/A 	|      N/A 	|
|    DT 	|             0.98 	|           0.48 	|             21.03 	|       0.27 	|     0.01 	|
|   SVM 	|             0.21 	|           0.19 	|            873.66 	|      10.63 	|     5.03 	|
|   KNN 	|             1.00 	|           0.60 	|             70.35 	|      70.43 	|     0.35 	|
|    NN 	|             0.31 	|           0.31 	|            149.89 	|       0.06 	|     0.03 	|

Overal the k-Nearest Neighbour model was the best. It had good training and validation F1-scores and quick to optimise and run.

The F1-scores for the Neural Network and Support Vector Machine were not acceptable.

The Decision tree performed well. However, overfitting to the trianing data resulted in a lower validation F!-score.


