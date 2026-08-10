Generalizing Decision Trees to Regressinon problems.

So far we have used the decision-tree learning algorithm to solve classification problems where the goals is to predict a discrete cetegory or class e.g given a set of features for an animal, predicting that the animal is a dog or a cat. What if we wanted to solve a regression problem; say given a set of features for a dog, predicting the price the dog can be sold for?

Calculate the reduction in variance of the target variable for each of the candidate split. Then select the candidate split with the largest reducation in variance. The Reduction in variance of the continous target value tells how good the split it. The larger the reduction the better. 


Variance Reduction = Parent Variance - Weighted Child Variance

>Here, I was initially confused because I was thinking why are we using the split with the largest variance? But the correct understanding is that we using the reduction in variance which comes from the smallest weighted variance in the child node values resulting from the split. The same understanding on Information Gain which is reduction in entropy. So the split with the minimum entropy (impurity) ie choose the split that leaves the class as homogenous as possible.

Repeat this process by recursively spliting each child node until the stopping criteria is reached ie maximum depth is reached or all examples belong to a single class. The predicted value can be calculated as the mean average of the