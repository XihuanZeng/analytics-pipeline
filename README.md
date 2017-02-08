# Analytics Pipeline

## Guidelines and Principles

The Machine Learning pipeline should have the following things

- Read data in and provide summary statistics
    - Show the distribution of each continuous variable 
    - Histograms of discrete variables
    
    
- Preprocessing 
    - Label Encoding
    - OneHot Encoding
    - Missing Value Imputation
    - Normalization


- Training ML algorithms with hyperparameter tuning
    - Random Forest
    - Linear/Logistic Regression with Lasso/Ridge 
    - Gradient Boosting
    - SVM
    - Model Stacking
    

- Analysis of Result

    - ROC curve, F1 score for each method
    
Note that for production purpose, we decide to use the standard packages from Anaconda, even that means our choice of packages are limited and some packages are outdated.

## Design Patterns

### Input 

For now, let's suppose the input is a csv file. Later we can generalize this to other format. 

We want to create a pipeline that can do some standatd works for general data regardless of context. We expect the data has categorical features and continuous features. We also expect the data is not perfect by having missing values, bad values or outliers.

### Output

We expect to create a pipeline(binary) that is fit once and predict multiple times whenever a new test set is coming.

### Reusability

We must take into consideration of how to store this pipeline object that is fitted by the training data. I sometimes have hard time with Python pickle when I store a complicated object, like a pipeline that consists of Sklearn LabelEnconder, OneHotEncoder, StandardScalar, Estimators or even nested Pipelines. This object just does not retrieve correctly in another session. So I tend to save different part of the pipeline separately in a train model directory.

# Expected Usage

Say we have train.csv and we have test1.csv, test2.csv... 

We train once with:

```sh
$ python analytics-pipeline --train train.csv
```

and log all parts of the pipeline into training folder.

Later we can run:

```sh
$ python analytics-pipeline --test test1.csv
$ python analytics-pipeline --test test2.csv
```

Or we can retrain the model

```sh
$ python analytics-pipeline --train train.csv,test1_with_label.csv,
```




