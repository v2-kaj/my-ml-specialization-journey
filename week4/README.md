TRAINING A NN in Tensorflow

model = Sequential(
    dense(units=12,activation="sigmoid")
    .
    .
    .

) This step specifies the architecture of the NN. It tells the mode how to compute the output of the layer given the input.

model.compile(loss=BinaryCrossentropy) This step specifies the loss function to be used for training.
The binaryCrossentropy loss function is used for binary classification problems. It is the logistic loss of -ylog(fx) - (1-y)log(1-fx)
If the problem is a regression problem then the loss function would be the MSE

model.fit(X,Y,ephochs=100) This is the step that the optimisation algo runs to minimise the loss function and find the values of the parameters (weights and biases) that minimise the loss. Tensorflow performs backpropagation to compute the gradients of the loss with respect to the parameters and updates the parameters using the gradients.
The epochs are the number of times the optimisation algo runs over the training data. Just like we hado numIters.

DETAILS
In Logistic regression for instance
Loss is computed over a single training example to understand how far the model prediction for x is from the the corresponding ground example y.

adn Cost is the average of the losses from all the examples

Other activation functions:
ReLu (Rectified Linear Unit)
Linear Activation Functions     

How do you choose the activation function.

For the output layer - depends on the target ground truth label y. eg if y is binary. then the actvation function for that is  sigmoid. For the continous value then activation function is linear. eg predict price of stocks which can go up to. negeative. for regression problems which the ground truth for y is a non-negtive values then ReLu.

For the hidden layers the most common choice is ReLu.. its faster to computer as sigmoid is slower. Another reason is that relu goes in only one part of the graph. while sigmoid goes flat in two places. for gradient descent this flat in only one part is faster.