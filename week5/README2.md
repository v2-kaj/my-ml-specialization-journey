EVALUATING PERFORMANCE OF A MODEL

Use a test set. 
But reporting the test set average error as the model's performance tends to be an optimistic evaluation the model's generalization error.

Use cross validation set. aka dev set. Choose a model that has the lowest cverrorr


Bias and Variance

High Bias (underfitting) - high cost ie Jtrain on the training data set
In other words, - the training error is higher than the baseline acceptable level of performance.

High variance (overfitting) - high cost on cross validation data set and  very low on Jtrain

Just right - Low on Jtrain and Jcv

How does regularization affect bias and variance.
Try different values of lambda and record the Jcv, pick the lambda that results in the lowesst Jcv

If the model has high bias, increasing the training examples doesnt improve the model's performance.

When you have high variance ie overfitting, getting more examples does help.

If the model has high variance (Overfitting)
- Increase Training Examples
- Reduce the number of features.
- Increase value of lambda in the regularization term

If model has high bias
- Increase the number of features eg the nunber of bedrroms
- Adding polynomial features eg area
- Reduce the value of lambda in the regularization term.

These are alittle confusing! :)

Bias/Variance in NN
Large (more layers or more units per layer) NN are low bias machines. The caveat is that large NN are computationally more expensive.

If it performs poorly on Jcv then get more examples.

High Variance(Overfitting) sort of relates to the model memorizig the training examples very well such that its training error ie (over the training set) is low but does fail to generalize to unseen examples eg the cross validation set.
