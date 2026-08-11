**Tree Ensembles**

One weakness of using a single decision tree is that it can be highly sensitive to small changes in the training data (overfits). with minor changes in the training data, we end up with different tree structures that ends up making different predictions. One way to ensure the algorithm is less sensitive (more robust to) to small changes is to build many trees called an ensemble of trees (collection of multiple of trees).An ensemble is a collection of models whose predictions are aggregated to produce a final prediction. This is why when using decision trees, you get better prediction accuracy (better generalization) when you use an ensemble of trees in many cases. Each of the trees in the ensemble makes a prediction on an observation and the majority prediction in the case of classification problems wins as the final prediction of the model.

How do you come up with several diverse (weakly correlated) trees? A statistical technique called Sampling with replacement is used.

Now that we have this technic of sampling with replacement which allows us to create bootstrapped training sets which we can use to build a tree ensemble algorithm eg the random forest algorithm (one powerful tree ensemble algorithm). Because we replace the selected observation before sampling the next observeation we can end up with repeated observations in the dataset and other observations may not even be present in some data sets. This is what precisely makes the datasets different.

Given a training set of size m
for b = 1 to B:
    Use sampling with replacement to create new training set of size m
    Train a decision tree on the bootstrap dataset.

B = the number of trees in the ensemble
This is known as bagged decision tree algorithm.

\[
\hat{y} = \text{majority vote of the trees' predictions}
\]

for classification problems, and

\[
\hat{y} = \frac{1}{B}\sum_{b=1}^{B} f_b(x)
\]

for regression problems.


There is one modification of this bagged decision tree algorithm to get an improved algorithm called Random forest. In random forest algorithm, at each split point only an randomly selected  subset of the features is considered as candidate features for spliting. This helps to reducec correlation among the trees.

>Q. Where does a ML engineer go camping? A. In a random forest :).
