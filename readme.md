# K-Nearest Neighbors & Credit Card Fraud

This project explores a credit card dataset labeled with instances of fraud and legitimate transactions. We will fit a K-Nearest Neighbors classification model to the data in order to predict fraud on the basis of the available features. In the process, we will also explore the benefits of feature selection.


## Motivation

The goal of this project is, primarily, to develop an intuitive understanding of the K-Nearest Neighbors algorithm both in concept and in practical application. As such, we will conclude this project without building and comparing additional types of models.


## About the Dataset

This project uses a credit card fraud dataset [available on Kaggle](https://https//www.kaggle.com/mlg-ulb/creditcardfraud).

**Kaggle Description**

The dataset contains transactions made by credit cards in September 2013 by European cardholders. It presents transactions that occurred in two days, where we have 492 frauds out of 284,807 transactions.

The dataset contains only numerical input variables which are the result of a PCA transformation. Features V1, V2, … V28 are the principal components obtained with PCA, the only features which have not been transformed with PCA are 'Time' and 'Amount'. Feature 'Time' contains the seconds elapsed between each transaction and the first transaction in the dataset. The feature 'Amount' is the transaction Amount, this feature can be used for example-dependent cost-sensitive learning. Feature 'Class' is the response variable and it takes value 1 in case of fraud and 0 otherwise.


## Results

We tested a number of K-Nearest Neighbors models using different scaling methods, feature sets, and both balanced and unbalanced data. We compared the results of each after hyperparameter optimization using GridSearchCV and selected the following settings for our final model:

**Scaling**<br />
Minmax

**Features**<br />
['V1', 'V2', 'V3', 'V4', 'V5', 'V6', 'V7', 'V9', 'V10', 'V11', 'V12', 'V14', 'V16', 'V17', 'V18']<br />
_These features were selected as they have a correlation coefficient >=30 or &lt;= -.30_

**n_neighbors**=3<br />
**weights**=’uniform’<br />
**metric**=’euclidean’<br />

**Accuracy**: 0.959390862944162<br />
**Recall**: 0.928571428571428<br />
**Precision**: 0.989130434782608<br />
**F1**: 0.957894736842105<br />
**AUC**: 0.978818800247371<br />

Settings and scores for additional models can be found in data/sub_results.csv and data/results.csv

When considering what is important in identifying credit card fraud, we pay special attention to Recall, as false negatives represent instances of fraud that we were unable to identify. In a practical sense, if we have cases of false positives, the cost is, potentially, an employee auditing a particular transaction whereas a false negative is an instance of successful theft.

We must also consider the results of our tests with the dataset using all features. While, in this instance, the best-performing model's scores are nearly identical to our feature-selected model's performance, we do run the risk of noise and less separability when we include features that do not contribute significantly to the final result. We would also see a greater appreciation for dimensionality reduction if working with a larger dataset. A trimmed dataset would see significantly faster training times by comparison to a dataset with more dimensions.
