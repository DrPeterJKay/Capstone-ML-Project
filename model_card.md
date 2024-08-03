# Model Card

See the [example Google model cards](https://modelcards.withgoogle.com/model-reports) for inspiration. 

## Model Description

### Overview:

The purpose of this model is to predict at a given point during the course (nominally 50% through) if a student is likely to withdraw from the course.
Students withdrawing are classed as "non-continuation" students and are reported by the university.
The model uses data from the VLE (Virtual Learning Environment), Student Assessment grades and Student Registration information systems to  make the predictions.
The data used to make the predictions was pre-processed. This was a three step process that included: cleaning the data, creating some new features and combining the three datasets.

### Input:

Numeric. The following inputs are required:
- Grade Mean (%): Mean of all the grades upto the threshold (nominally 50% of the way through the course)
- Grade Standard Deviation (%): Standard Deviation of all the grades upto the threshold (nominally 50% of the way through the course)
- VLE Mean (-/day): Mean of the number of daily interactions with the VLE (Virtual Learning Environment) upto the threshold (nominally 50% of the way through the course)
- VLE Standard Deviation (-/day):  Standard Deviation of the number of daily interactions with the VLE upto the threshold (nominally 50% of the way through the course)

### Output:

A binary prediction if a student is likely to withdraw (1) or not (0)

### Model Architecture:

There is significant pre-processing of the data needed.
There are three data sources that need to be combined. The data sets are VLE engagement, Assessment Grades and Student Registration data.
First, each data file is cleaned to remove any row entries that have blank fields.
The VLE and Assessment data sets are truncated to only include data upto the defined threshold.
The default threshold used is 50% of the course duration.

After cleaning the data four models were optimised and trained. The four models and the hyperparameters for each model that were optimised are presented below:

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

In all cases I used a grid search methodology to optimise the hyperparameters. This is mainly because the optimisiation time for the models was relatively short in duration (longest was approximately 15 minutes).

A final Naive model (Model 0) was created to benchmark each of the other models. This was a DummyClassifier with a stratified strategy.

## Performance:

Give a summary graph or metrics of how the model performs. Remember to include how you are measuring the performance and what data you analysed it on. 

The F1-score has been chosen as the metric to compare model performance and to optimise the models.

This was selected for a few reasons. First, the data set is imbalenced, therefore accuracy is not appropriate.
Secondly, from a practical point of view the resource to intervene with students are finite, therefore using on students that don't need it (False Positive) or missing stundents that do need it (False Negative) is detrimental. F1-score is a combination of these and therefore a good metric for this problem.

The table below summarises the results:

| Model 	| F1-score (train) 	| F1-score (val) 	| Optimisation Time 	| Train Time 	| Run Time 	|
|------:	|-----------------:	|---------------:	|------------------:	|-----------:	|---------:	|
| Naive 	|              N/A 	|           0.16 	|               N/A 	|        N/A 	|      N/A 	|
|    DT 	|             0.98 	|           0.48 	|             21.03 	|       0.27 	|     0.01 	|
|   SVM 	|             0.21 	|           0.19 	|            873.66 	|      10.63 	|     5.03 	|
|   KNN 	|             1.00 	|           0.60 	|             70.35 	|      70.43 	|     0.35 	|
|    NN 	|             0.31 	|           0.31 	|            149.89 	|       0.06 	|     0.03 	|

## Limitations:

This model has been trained on data from the Open University.
The OU is an online university and potentially has a different learner profile to 'in-person' universities.
Therefore, if using data from a more traditional in-person University then the exercise should be repeated to check which model is more appropriate.

## Trade-offs:

Overall the k-Nearest Neighbour model was the best. It had good training and validation F1-scores and was quick to optimise and run.

The F1-scores for the Neural Network and Support Vector Machine were not acceptable.

The Decision tree performed well. However, overfitting to the training data resulted in a lower validation F1-score.

## Bias and Equity:

Users should be aware that as with every model, bias is a known risk and can be linked to factors such as the size, diversity, and quality of data sets, as well as existing social and structural inequities.

Although data were available about student's backgrounds (age, gender, class, etc) it was decided, for this project, to remove these features from the modelling. This is for a few reasons, first your background and characteristics should not determine your probability of withdrawing. Secondly, this risks breaking GPDR data regulations. Students provide information about their background for reporting purposes only. To use this to single them out for intervention is not ethical.
