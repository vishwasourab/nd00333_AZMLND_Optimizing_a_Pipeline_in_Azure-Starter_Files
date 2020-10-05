# Optimizing an ML Pipeline in Azure

## Overview
This project is part of the Udacity Azure ML Nanodegree.
In this project, we build and optimize an Azure ML pipeline using the Python SDK and a provided Scikit-learn model.
This model is then compared to an Azure AutoML run.

## Summary
**In 1-2 sentences, explain the problem statement: e.g "This dataset contains data about... we seek to predict..."**

This dataset contains data about bank telemarketing. The dataset has 21 columns and about 32000 rows. We're trying to predict the column named 'y' which has two class possibilities (yes, no). There is heavy class imbalance in the dataset. There are less than 3200 'yes' records which accounts to around 10% of the total rows.

**In 1-2 sentences, explain the solution: e.g. "The best performing model was a ..."**

The best performing model was a VotingEnsemble model built by AutoML. This has an accuracy of 91.72%. The model used the engineered features. The numerical features were imputed using the mean and the categorical were label encoded and vectorized.

## Scikit-learn Pipeline
**Explain the pipeline architecture, including data, hyperparameter tuning, and classification algorithm.**

The training pipeline for SKLearn model is as follows:
* Load the data from TabularDatasetFactory
* Clean the dataset using predefined function named **clean_data**
  * One Hot Encode the categorical columns
  * Separate the features and target
* Split the dataset into train and test sets
* Build a Logistic Regression model
* Tune hyperparameters using Hyperdrive
* Select the best model from the tuning
* Save and register the model for the later use 

**What are the benefits of the parameter sampler you chose?**

I have chosen Random Sampling to choose the hyperparameters. This type of sampling is good for initial experiments and we can refine our search space in later experiments. 

Random Sampling
* Supports discrete and continuous hyperparameters
* Supports early termination of low performance runs

**What are the benefits of the early stopping policy you chose?**

I choose Bandit Policy for early termination. This policy takes **slack_factor or slack_amount** as an input and any run that doesn't fall within the slack factor or slack amount of the evaluation metric with respect to the best performing run will be terminated.

Example:

Consider a Bandit policy with slack_amount = 0.1 and evaluation_interval = 100. If Run 3 is the currently best performing run with an AUC (performance metric) of 0.8 after 100 intervals, then any run with an AUC less than 0.7 (0.8 - 0.1) after 100 iterations will be terminated. Similarly, the delay_evaluation can also be used to delay the first termination policy evaluation for a specific number of sequences.

## AutoML
**In 1-2 sentences, describe the model and hyperparameters generated by AutoML.**

## Pipeline comparison
**Compare the two models and their performance. What are the differences in accuracy? In architecture? If there was a difference, why do you think there was one?**

## Future work
**What are some areas of improvement for future experiments? Why might these improvements help the model?**

## Proof of cluster clean up
**If you did not delete your compute cluster in the code, please complete this section. Otherwise, delete this section.**
**Image of cluster marked for deletion**
