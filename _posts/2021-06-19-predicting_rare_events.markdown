---
layout: post
title:      "Predicting Rare Events"
date:       2021-06-19 20:09:25 +0000
permalink:  predicting_rare_events
---


Today, I will be talking about building a model to identify rare events (client churn or diseases, for example). This business problem is prevalent, and reducing those events can mean lives being saved or higher profits.

## Approach of building a Model

The main problem of building a predictor for these events is that they are rare. Therefore, the model needs to be capable of finding these exceptions in a sea of non-rare events. To achieve that, there are three main things we have to do:

### Dealing with an Unbalanced Set - Oversampling

When working with rare events, we are dealing with an unbalanced dataset which means that most of the data is non-rare events. The consequence of working with such a dataset is that a model can be very performant by predicting all events as "non-rare" since most of the dataset is composed of those types of events. Therefore, it's necessary to perform oversampling of the rare event, so we have a balanced dataset.

### Picking the correct Metric to optimize

When dealing with this type of problem, it's important to choose the correct Metric to optimize. Most of the time, we use the **Accuracy Score** to train the model and identify the top performer. However, in the case of rare events, it makes more sense to use the **Recall Score** which measures the ability of the model to predict True Positive from all True Positives in the data set (the calculation is: *True Positive / (True Positive + False Negatives)*. By maximizing that score, we are aiming for success.

### The True/False Positives Trade-Off

Since the goal is to find those rare instances, we might end up being ultra-conservative. The consequence of that is a model that will predict all events are rare, which is non-sense. So instead, it's necessary to understand the business case and decide the right balance of True/False Positives.

For example, if we are talking about predicting diabetes since the risk of missing a True Positive might cost someone's life, it makes sense to be conservative and have more False Positives.

However, suppose we are predicting the chance of a customer to churn. In that case, we might want to consider not having as many False Positives because that would be very costly for the company, assuming that the prediction would trigger some action (emailing or calling these clients, for example).

Therefore, while building the model, think through the business problem and apply best judgment. Understanding the consequences of an extra True/False Positive can be helpful. While it's hard to put a price on someone's, we also don't want to predict every single patient as positive for diabetes. However, sometimes we can estimate the additional cost of having more False Positives to capture a few more True Positives.

## Conclusion

Like in any project, the most important thing to know is the business case and the implications of your work to the business.  Specifically, in the scenario of predicting rare events, it will decide whether the model has to be more conservative or not. With that in mind, it's a matter of analyzing the Recall Score and the True/False Positive balance and decide which setup provides the best trade-off.

