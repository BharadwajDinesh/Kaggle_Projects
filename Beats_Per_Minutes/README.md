
# Predicting the Beats-per-Minute of Songs

This repository contains my complete workflow for the Kaggle Playground Series (September 2025) competition, where the goal is to predict the beats-per-minute (BPM) of songs using a synthetic tabular dataset.


## Data Description

The dataset for this competition (both train and test) was generated from a deep learning model trained on the BPM Prediction Challenge dataset. Feature distributions are close to, but not exactly the same, as the original. Feel free to use the original dataset as part of this competition, both to explore differences as well as to see whether incorporating the original in training improves model performance.

Files 
train.csv - the training dataset; BeatsPerMinute is the continuous target ground truth

test.csv - the test dataset; your objective is to predict the BeatsPerMinute for each row
sample_submission.csv - a sample submission file in the correct format
## Approach

I began the baseline experimentation by training the dataset using a simple Linear Regression model. This provided an initial benchmark, achieving an accuracy score of **26.39266**. While the baseline helped establish a starting point, it clearly indicated significant room for improvement.

To enhance performance, I trained the data on multiple regression algorithms, each offering different strengths in handling feature interactions, non-linearity, and regularization. After comparing their results, the most promising performance was achieved using CatBoost **26.38902**, which delivered the highest accuracy among all tested models.

CatBoost’s ability to handle complex relationships, reduce overfitting, and work efficiently with minimal preprocessing made it the standout choice for this task.
### Model Accuracy

| Model     | Accuracy | 
| :-------- | :------- | 
| `Liear Regression` | `26.39266` | 
| `Lasso Regression` | `26.39388` |
| `Ridge Regression` | `26.39241` | 
| `ElasticNet` | `26.39222`|
| `CatBoost` | `26.38902` | 

