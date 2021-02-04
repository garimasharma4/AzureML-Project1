# Optimizing an ML Pipeline in Azure

## Overview
This project is part of the Udacity Azure Machine Learning (ML) Nanodegree.
In this project, we build and optimize an Azure ML pipeline using the Python SDK and a provided Scikit-learn model.
This model is then compared to an Azure AutoML run.

## Summary

**Problem statement:**

For this project, we were provided a Bank's Marketing data. Based on my research on this dataset, the data is related to telemarketing campaigns for a Portugese banking institution. There are 32,950 unique records with details such as age, job, marital status, education, loan history and data related to the campaign. We seek to predict whether or not the client will subscribe to a term deposit with the bank. This is a classification problem with two classes - yes or no, thus making it a binary classification problem.

**Solution overview and the outcome:**

Two approaches were taken to solve this binary classification problem:
1. Custom-coded standard scikit-learn regression model. It's hyperparamters were optimised using the MS Azure ML HyperDrive.
2. Build and optimise the best performing model using AutoML.

Out of the above two approaches, approach #2 (the AutoML run) helped find the best performing model that is the Voting Ensemble. It had an accuracy of 0.9168. The accuracy of the scikit-learn regression model from the first approach was 0.9118.

## Scikit-learn Pipeline

### Scikit-learn pipeline architecture

![alt text](https://github.com/garimasharma4/AzureML/blob/master/Architecture%20Diagram%20Project%201.png?raw=false)

### Data

### Hyperparameter tuning
Hyperparameter tuning along with AutoML can help dramatically speed up the development of models in MS Azure ML. Hyperparameters are adjustable parameters that we choose for model training. They let us control the model training process. Hyperparameter tuning is finding that set of hyperparameters (that configuration of hyperparameters) that results in the best performance of the trained model. With the help of packages such as HyperDrive from MS Azure ML, we can efficiently automate hyperparameter tuning.

**Benefits of chosen parameter sampler**

MS Azure ML supports the following sampling methods. For this project, we used random sampling over the hyperparameter space.
1. Random sampling
2. Grid sampling
3. Bayesian sampling

In random sampling, hyperparamter values are randomly selected from the defined search space. The benefits of random sampling are:
1. It supports discrete and continuous hyperparameters.
2. It supports early termination of low-performance runs.
3. In short amount of time, we can achieve excellent results.

In the code, we defined a search space with two parameters - C parameter (inverse of the regularisation strength) and maximum number of iterations to converge.

**Benefits of the chosen early stopping policy**

As the name suggests, early termination policy allows us to configure parameters that decide when to automatically terminate runs that are performing poorly. The early termination policy used for this project is Bandit Policy. It is based on slack criteria, frequency (optional) and the delay interval for evaluation (optional). Slack is the slack/leniency allowed with respect to the best performing training run. It could be **slack amount** that specifies the allowed slack as the exact amount or it could be **slack factor** that specifies allowed slack as a ratio. An early termination policy helps improves the computational efficiency.

### Classification algorithm

## AutoML
**In 1-2 sentences, describe the model and hyperparameters generated by AutoML.**
Compared to the scikit-learn logistic regression model, AutoML was reasonably simple to execute. It gave the best performing model in a considerably short period at an accuracy of .9168. Below is a description of the AutoML model and its hyperparameters:

The dataset was created by using the TabularDatasetFactory. Then the clean_data method was called to perform the data preparation and one hot encoding on that dataset. Then, a dataframe was created that was passed as one of the parameters to the AutoMLConfig constructor. In the AutoMLConfig constructor, label column ('y') was also provided along with the primary metric ('accuracy') and problem task i.e. ('classification'). The hyperparameters generated by AutoML model are:


## Pipeline comparison
In this project, it was the scikit-learn logistic regression model versus the AutoML. While the second approach gave us the best performing model after considering multiple models (VotingEnsemble accuracy .9168), with the first one, we were working with only one model, i.e. scikit-learn logistic regression model. For that, we could only optimise it’s hyperparameters and thus not able to improve it’s accuracy more than .9118. In my opinion, AutoML offers more flexibility to choose from a vast list of algorithms.

## Future work
**What are some areas of improvement for future experiments? Why might these improvements help the model?**

## Proof of cluster clean up
**If you did not delete your compute cluster in the code, please complete this section. Otherwise, delete this section.**
**Image of cluster marked for deletion**
