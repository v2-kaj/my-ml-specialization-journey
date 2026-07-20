Multiclass Classification.

Recall that Logistic Regression applies when y can take on two possible values. Thus we use Logistic regression to solve binary classification problems.

In logistic regression we compute the probability that y = 1 given x. P(y=1|x) as follows:

z = W^T * X + b

a = g(z) = 1/(1+e^(-z)) and we interpret a as the probability that y = 1 given x.

where g is the sigmoid function: g(z) = 1 / (1 + e^(-z))

Thus if the a1, P(y=1|x) = 0.7 then the probability of y being 0 given x is 0.3 since the sum of all probabilities must be equal to 1. a2 = 1 - a1

Now let's generalize this to the softmax regression for multiclass classification. Let's use a concrete example of when y can be 1, 2, 3 or 4.

z1 = W1^T * X + b1
z2 = W2^T * X + b2
z3 = W3^T * X + b3
z4 = W4^T * X + b4

Remember w1, w2, w3, w4 are vectors and b1, b2, b3, b4 are scalars are parameters of softmax regression.

Then;

a1 = e^z1 / (e^z1 + e^z2 + e^z3 + e^z4)
a2 = e^z2 / (e^z1 + e^z2 + e^z3 + e^z4)
a3 = e^z3 / (e^z1 + e^z2 + e^z3 + e^z4)
a4 = e^z4 / (e^z1 + e^z2 + e^z3 + e^z4)


a1 is the probability that y = 1 given input features x.
a2 is the probability that y = 2 given input features x.
a3 is the probability that y = 3 given input features x.
a4 is the probability that y = 4 given input features x.

Now for the general case where y can be 1,2,3,...,N

zj = Wj^T * X + bj for j = 1, 2, 3, ..., N
parameters are w1, w2, ..., wN and b1, b2, ..., bN

and;

aj = e^zj / Σ(e^zk) for k = 1 to N where aj represents the probability that y = j given input features x.

When N = 2 then softmax regression ends up being logistic regression.

Cost function for Softmax Regression

Recall that for logistic regression we have:

z = w^T * x + b

a1 = g(z) = 1 / (1 + e^(-z))

and the P(y=1|x) = a1, a2 = P(y=0|x) = 1 - a1

loss = -ylog(a1) - (1 - y)log(1 - a1)

Jwb  = average loss for the entire training set.

For Sotfmax regression, we have:

Loss(a1,...aN, y) = {
    -loga1 if y=1,
    -logaN if y=N
    -loga2 if y=2,
    ...
}

Now let's see how softmax is used in Neural Networks to solve multiclass classification problems.
Neural Network with softmax output.




