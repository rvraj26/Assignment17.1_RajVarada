# UCB ML/AI Certification: Practical Assignment 17.1

# Business Objective of the Project

## Business Objective  
The business objective is to improve the effectiveness of a Portuguese bank's marketing efforts conducted over the telephone. The goal of the marketing effort is to get the customer to subscribe to a long-term product and reduce the cost of these efforts (customer acquisition cost). The primary objective of this assignment is to build a predictive model that can classify whether a customer contacted on the phone as part of this marketing campaign will sign up for the deposit product. This will help the bank to focus on customers with an excellent chance to sign up, to increase the percentage of customers who start a term deposit as a result of the campaign (effectiveness), and reduce the acquisition cost.
  
## Problem Statement  
This classification problem with the objective to identify the most predictive features influencing the classification outcome. The solution will compare the performance of different classification algorithms - k-nearest neighbors, logistic regression, decision trees, and support vector machines, to determine which model best predicts client subscription.


# Data Understanding and Preparation

## Data Understanding  
The dataset is sourced from the UCI Machine Learning repository, https://archive.ics.uci.edu/dataset/222/bank+marketing. It contains data from marketing campaigns conducted by a Portuguese bank between May 2008 and November 2010. The dataset has 41188 entries and 21 features, covering client information, contact details, and social and economic context attributes. The target variable indicates if the client subscribed to the term deposit. Four data files with slightly differing content were provided. I used bank-additional.csv with 4119 (10%) entries for developing the code, and the bank-additional-full.csv with 41188 (100%) entries for the final results. 
  
The features in the dataset showed four different sets of characteristics: data related to the customer the bank contacted in the campaign, information related to the last time the customer was contacted during the campaign, the campaign outcome, and some economic features. 
  
## Data Preparation
None of the columns have missing values.
There are no duplicate entries.
There are 21 features - 10 numeric and 11 categorical
The categorical features can be updated as follows: 
a. Three features, default, housing, and loan, are yes/no values and can be converted to numeric 1/0 if needed 
b. Two features, month and day_of_week, can be converted to a number, 1..12 and 1..7, respectively. 
c. The rest of the categorical features can be encoded with One Hot Encoding
The numeric features can be scaled using StandardScalar.
  
  
As indicated in the assignment, the data was split into train and test datasets, with a 70% -30 % split for features 1-7. 
  
# Methodology:

Initially, a baseline model using DummyClassifier with no optimization was built. All future results are compared to this baseline model. 
  
Next, basic Logistic Regression and Decision Tree models were built. The results were compared to the Dummy Classifier model, and they did not show any improvement. 
  
After this initial model builds, exploratory data analysis (EDA) and feature engineering methods were applied. All the features were plotted to identify patterns to use. Based on this, I simplified some features by making them binary.
  
is_employed: map all employed types to 1. All others mapped to 0
is_married: map married to 1. divorced, single, and unknown to 0
age_cat: map age to buckets of 10 years
housing: map yes to 1. no and unknown to 0
loan: map yes to 1. no and unknown to 0
default: There are a large number of unknowns and only three yes's. Drop this column
education: The results improved without education. So, dropping that column. Look at this for future work.
  
All the new features were visualized again. The three new features, is_employed, is_married, and age_cat, were used in place of job, marital, and age in further analysis. 
  
The data was split into train and test datasets, with a 70% -30 % split for all features. 
  
Build the four estimators, LR, DT, SVN, and KNN, and score their run time and accuracy.
The results didn't change much.
  
Next, a few more features from the original dataset were added back, and the models were rebuilt. The results improved, indicating that the right feature set and transformations for the best results had been identified. This can be used to tune the hyper parameters using grid search.
  
# Results

A Decision Tree with a max_depth of 4 provided the highest train and test accuracy with minimal training time. This model beats the accuracy of the baseline model by around 3%.

Model	Best Estimator	Train Time	Train Accuracy	Test Accuracy
0	Logistic Regression	LogisticRegression()	0.318884	0.911529	0.908524
1	Decision Tree	DecisionTreeClassifier(max_depth=4)	0.158806	0.914617	0.910791
2	Support Vector Machine	SVC(gamma=0, kernel='linear')	52.330370	0.905041	0.904881
3	K Nearest Neighbors	KNeighborsClassifier(n_neighbors=np.int64(29))	0.012608	0.912049	0.907715

Confusion Metric for Decision Tress 
  
I computed the AUC, and it shows that the Logistic Regression model has a better AUC of 0.94 which is better than the AUC of 0.91 of the Decision Tree model, even though Decision Tree has better accuracy than Logistic Regression.

# Deployment
1. The bank is recommended to use the methods and results from the final decision tree model as it gives the best accuracy score
2. The Jupyter Notebook for this assignment is checked into the Git Hub repository at https://github.com/rvraj26/Assignment17.1_RajVarada

# Future work
1. Adding dropped features to the outcome must be explored.   
2. One feature set, `education`, should be explored. The feature has many categories of values, and it could yield a wealth of information.  
