This week, I learn about Logistic Regression.

The name is a bit misleading because while it is called "Regression", it is actually used for classification problems and not regression problems.

Recall how there are two types of supervised learning problems:
- Regression 
- Classification

In classification problem, our goal is to predict a discrete label (0 or 1, true or false, etc.) from a finite set of categories aka classes. On the other hand, in regression problems, our goal is to predict a continuous value (like price, temperature, etc.)

Logistic Regression.
It turns out that linear regression is not suitable for classification problems as it can produce values outside the range [0, 1].

Lets build up to logistic regression step by step.

There's a mathematical function called the sigmoid function that can map any real number z to the range [0, 1].

g(z) = 1 / (1 + e^(-z))

This function is also known as the logistic function.

Notice how whenever the the value of z is a large negative number, the output of the function approaches 0. And whenever the value of z is a large positive number, the output of the function approaches 1.

In logistic regression, we use this function to map the output of a linear function to a probability value between 0 and 1.

Recall from linear regression that:
fwb(x) = wx + b 


Now in logistic regresssion we can write:
fwb(x) = g(wx + b) where g is the sigmoid function and z = wx + b

The above is assumming w,z and b are scalars. But the principle remains the same for vectors.

So for vectors, we can write:
fwb(x) = g(w^T x + b) where w and x are vectors and b is a scalar.
Thus z = w^T x + b

Given this, we can predict categories between 0 and 1 using the logistic function fwb(x) = g(w^T x + b) where g is the sigmoid function and z = w^T x + b. Thus g(z) = 1 / (1 + e^(-z)) giving us a probability value between 0 and 1.

COST FUNCTION FOR LOGISTIC REGRESSION

Recall that a cost function give us a mesure of how well our set of parameters (w and b) are performing. In other words, it tells us how well our model is fitting the training data.

As you can recall that in linear regression, we used the mean squared error (MSE) as our cost function. But in logistic regression, we use a different cost function because the MSE cost function is not suitable for logistic regression.

our MSE cost function for logistic regression is:
jwb =  1/2m * Σ(i=1 to m) (fwb(x^(i)) - y^(i))^2

where fwb(x^(i)) = w^T x^(i) + b is the predicted value and y^(i) is the actual value in our training set.

[I've skiepped some mathematical build up to below]

Now for logistic regression, the cost function is;

jwb = -1/m * Σ(i=1 to m)[y^(i)log(fwb(x^(i)) + (1 - y^(i))log(1 -fwb(x^(i))))]

This function has the nice property that it is convex and so we can use gradient descent to find the optimal parameters ie the values of w and b that minimize the cost function.

Recall that the cost function for logistic regression is jwb = 1/m * Σ(i=1 to m) [loss(fwb(x^(i)), y^(i))]

where loss of fwb(x^(i)), y^(i) is defined as:
loss(fwb(x^(i)), y^(i)) = -[y^(i)log(fwb(x^(i))) + (1 - y^(i))log(1 - fwb(x^(i)))]

where fwb(x^(i)) = g(w^T x^(i) + b) thus z^(i) = w^T x^(i) + b and predicted y^(i) = 1/(1+e^(-z^(i)))

Note that loss is defined as how wrong our prediction is for a single given training example but calculate by summing over all training examples. Cost on the other hand is the average of the loss over all training examples.

Now to implement this in pseudo code:
compute cost(X,y,w,b):
    initiaze cost = 0
    m = shape of x[0]
    for i starting from 0 to m:
        fwbxi = w.T * x[i] + b which is the dot product
        yhati = g(fwbxi) ie 1/(1 + e^(-fwbxi)) which is the sigmoid function
        cost += -y[i] * log(yhati) - (1 - y[i]) * log(1 - yhati)
    return cost/m

To test this we can compute the cost for a given set of parameters w and b. say w = [0, 0] and b = 0 for a cost of say 0.443
if you choose another set of parameters say w = [1, 1] and b = 1 for a cost of say 0.234 you can see visually that the decision boundary line would be better for a choice of the latter as your set of parameters. This shows that the cost function is a good measure of how well our model is performing.

Now to calculate gradient descent for the logistic function:

djdw = 1/m * Σ(i=1 to m) (fwb(x^(i)) - y^(i)) * xj^(i)

djdb = 1/m * Σ(i=1 to m) (fwb(x^(i)) - y^(i))

and logistic regression becomes:
repeat until convergence:
wj = wj - α * djdw
bj = bj - α * djdb
permforming simultaneous update ofcours.

so in pseudo code
compute gradient for logistic(X, y, w, b):
    initialize djdw = [0, 0, ..., n] where n is the number of features
    initialize djdb = 0

    for i from 0 to m:
        z = w.T * x[i] + b where w.T is the transpose of w and x[i] is the i-th training example so we performing the dot product
        fwbxi = g(z) ie 1/(1 + e^(-z)) which is the sigmoid function
        for j from 1 to n:
            djdw[j] = djdw[j] + (fwbxi - y[i]) * x[i,j]
        djdb = djdb + (fwbxi - y[i])
    return djdw/m, djdb/m

Take a look at my python implementation of compute_gradient_logistic in the jupyter notebook

Now gradient descent for logistic regression:
compute gradient descent for logistic(X,y,win,bin,alpha,num_iters):
    w = win
    b = bin
    for i in range from 0 to num_iters:
        djdw, djdb = compute_gradient_logistic(X, y, w, b)
        w = w - alpha * djdw
        b = b - alpha * djdb
    return w, b

to have the cost at each iteration we can modify the function to return the cost as well:
cost = []
for i in range from 0 to num_iters:
    cost[i] = compute_cost_logistic(X, y, w, b)
    djdw, djdb = compute_gradient_logistic(X, y, w, b)
    w = w - alpha * djdw
    b = b - alpha * djdb
return w, b, cost

Now we can plot how the cost changes with each iteration to see if our model is converging. Note that the first value in the cost is the cost at first iteration and the last value in the cost is the cost at last iteration. For large values of num_iters, lets not compute the cost at each iteration to save time. For debugging purposes just to see  if our model is converging, we can compute the cost only for the first 100 iterations.

so the modified function would look like:
compute gradient descent for logistic(X,y,win,bin,alpha,num_iters):
    w = win
    b = bin
    cost = []
    for i in range from 0 to num_iters:
        if i < 100:
            cost.append(compute_cost_logistic(X, y, w, b))
        djdw, djdb = compute_gradient_logistic(X, y, w, b)
        w = w - alpha * djdw
        b = b - alpha * djdb
    return w, b, cost





