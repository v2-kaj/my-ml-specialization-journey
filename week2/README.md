This week, I learned about Logistic Regression.

The name is a bit misleading because while it is called "Regression", it is actually used for classification problems and not regression problems.

Recall how there are two types of supervised learning problems:
- Regression 
- Classification

In classification problem, our goal is to predict a discrete label (0 or 1, true or false, etc.) from a finite set of categories aka classes. On the other hand, in regression problems, our goal is to predict a continuous value (like price, temperature, etc.)

Logistic Regression.
It turns out that linear regression is not suitable for classification problems as it can produce values outside the range [0, 1].

Lets build up to logistic regression step by step.

There's a mathematical function called the sigmoid function that can map any real number to the range [0, 1].

g(z) = 1 / (1 + e^(-z))

This function is also known as the logistic function.

Notice how whenever the the value of z is a large negative number, the output of the function approaches 0. And whenever the value of z is a large positive number, the output of the function approaches 1.


In logistic regression, we use this function to map the output of a linear function to a probability value between 0 and 1.

Recall from linear regression that:
fwb(x) = wx + b 


Now in logistic regresssion we can write:
fwb(x) = g(wx + b) where g is the sigmoid function.

This means that z = wx + b

The above is assumming w,z and b are scalars. But the principle remains the same for vectors and matrices.

So for vectors and matrices, we can write:
fwb(x) = g(w^T x + b) where w and x are vectors and b is a scalar.
Thus z = w^T x + b

Given this, we can predict categories between 0 and 1.

COST FUNCTION FOR LOGISTIC REGRESSION

Recall that a cost function give us a mesure of how well our set of parameters (w and b) are performing. In other words, it tells us how well our model is fitting the training data.

As you can recall that in linear regression, we used the mean squared error (MSE) as our cost function. But in logistic regression, we use a different cost function because the MSE cost function is not suitable for logistic regression.

our MSE cost function for logistic regression is:
jwb =  1/2m * Σ(i=1 to m) (fwb(x^(i)) - y^(i))^2

where fwb(x^(i)) = w^T x^(i) + b is the predicted value and y^(i) is the actual value in our training set.




