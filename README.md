# Improved-Hybrid-Feature-Selection-Techniques

**In this project we design various advanced feature selection techniques for selecting the most optimal features for any machine learning model. The code is written in such a manner that it can be incorporated to any data science pipeline. In the below section we give all the details about the approach.**

## Important Note

In all feature selection procedures, it is good practice to select the features by examining only the training set. And this is to avoid overfit.
You have to separate train and test sets first before going for feature selection

## To speed things up it is recommended to apply some quick filter methods of feature selection at the initial stage right after train_test_split. We do the following

* Remove constant, quasi-constand and duplicated features.

### Recursive feature addition

This method consists of the following steps:

1) Rank the features according to their importance derived from a machine learning algorithm: it can be tree importance or coefficients from linear models.

2) Build a machine learning model with only 1 feature, the most important one, and calculate the model metric for performance.

3) Add one feature -the most important- and build a machine learning algorithm utilising the added and any feature from previous rounds.

4) Calculate a performance metric of your choice: roc-auc, mse, rmse, accuracy, etc.

5) If the metric increases by more than an arbitrarily set threshold, then that feature is important and should be kept. Otherwise, we can remove that feature.

6) Repeat steps 2-5 until all features have been evaluated.


I call this a hybrid method because:

- it derives the importance derived from the machine learning algorithm, like embedded methods
- it builds several machine learning models, like wrapper methods.

This method is faster than wrapper methods and often better than embedded methods. In practice it works extremely well. 

One thing to note is that the minimum drop in performance to decide if a feature should be kept is set arbitrarily. The smaller the drop the more features will be selected, and vice versa.

**Model Used for Demonstration: GradientBoostingClassifier, GradientBoostingRegressor**



