# Improved-Hybrid-Feature-Selection-Techniques

**In this project we design various advanced feature selection techniques for selecting the most optimal features for any machine learning model. The code is written in such a manner that it can be incorporated to any data science pipeline. In the below section we give all the details about the approach.**

## Important Note

* In all feature selection procedures, it is good practice to select the features by examining only the training set. And this is to avoid overfit.
You have to separate train and test sets first before going for feature selection.

* In practice, feature selection should be done after data pre-processing. So ideally, all the categorical variables are encoded into numbers, and then you can assess how deterministic they are of the target.

* To speed things up it is recommended to apply some quick filter methods of feature selection at the initial stage right after train_test_split. We do the following: Remove constant, quasi-constand and duplicated features.

### Recursive feature addition

This method consists of the following steps:

1) Rank the features according to their importance derived from a machine learning algorithm: it can be tree importance or coefficients from linear models.

2) Build a machine learning model with only 1 feature, the most important one, and calculate the model metric for performance.

3) Add one feature -the most important- and build a machine learning algorithm utilising the added and any feature from previous rounds.

4) Calculate a performance metric of your choice: roc-auc, mse, rmse, accuracy, etc.

5) If the metric increases by more than an arbitrarily set threshold, then that feature is important and should be kept. Otherwise, we can remove that feature.

6) Repeat steps 2-5 until all features have been evaluated.

I call this a hybrid method because:

it derives the importance derived from the machine learning algorithm, like embedded methods.
it builds several machine learning models, like wrapper methods.
This method is faster than wrapper methods and often better than embedded methods. In practice it works extremely well.

One thing to note is that the minimum drop in performance to decide if a feature should be kept is set arbitrarily. The smaller the drop the more features will be selected, and vice versa.

**Model Used for Demonstration: GradientBoostingClassifier, GradientBoostingRegressor**

### Feature Selection by Random Shuffling

This approach of feature selection consists in random shuffling the values of a specific variable and determining how that permutation affects the performance metric of the machine learning algorithm. In other words, the idea is to permute the values of each feature, one feature at the time, and measure how much the permutation (or shuffling of its values) decreases the accuracy, or the roc_auc, or the mse of the machine learning model (or any other performance metric!). If the variables are important, a random permutation of their values will decrease dramatically any of these metrics. Contrarily, the permutation or shuffling of values should have little to no effect on the model performance metric we are assessing.

The procedure goes more or less like this:

- Build a machine learning model and store its performance metric
- Shuffle 1 feature, and make a new prediction using the previous model
- Determine the performance of this prediction
- Determine the change in the performance of the prediction with the shuffled feature vs the original one
- Repeat for each feature

To select features, we choose those that induced a decrease in model performance, beyond an arbitrarily set threshold.

Here I have demonstrated how to select features based on random shuffling on a regression and classification problem. 

**Note For the demonstration, I have used Random Forests, but this selection procedure can be used with any machine learning algorithm. In fact, the importance of the features are determined specifically for the algorithm used. Therefore, different algorithms may return different subsets of important features.**



