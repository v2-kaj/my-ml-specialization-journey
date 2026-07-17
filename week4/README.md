TRAINING A NN in Tensorflow

model = Sequential(
    dense(units=12,activation="sigmoid")
    .
    .
    .

) This step specifies the architecture of the NN. It tells the model how to compute the output of the layer given the input.

model.compile(loss=BinaryCrossentropy) This step specifies the loss function to be used for training.
The binaryCrossentropy loss function is used for binary classification problems. It is the logistic loss of -ylog(fx) - (1-y)log(1-fx)
If the problem is a regression problem then the loss function would be the MSE

model.fit(X,Y,ephochs=100) This is the number of steps that the optimisation algo runs to minimise the loss function and find the values of the parameters (weights and biases) that minimise the loss. Tensorflow performs backpropagation to compute the gradients of the loss with respect to the parameters and updates the parameters using the gradients.
The epochs are the number of times the optimisation algo runs over the training data. Just like we hado numIters.

DETAILS
In Logistic regression for instance
Loss is computed over a single training example to understand how far the model prediction for x is from the the corresponding ground example y.

And Cost, J, is the average of the losses from all the examples

Other activation functions apart from sigmoid:
ReLu (Rectified Linear Unit)
Linear Activation Functions     

How do you choose the activation function.

For the output layer - depends on the target ground truth label y. eg if y is binary. then the activation function for that is sigmoid. For the continous value which can be negative values then the appropriate activation function is linear. e.g price of stocks. For regression problems in which the ground truth for y is a non-negtive values then ReLu.

For the hidden layers the most common choice is ReLu.. its faster to computer as sigmoid is slower. Another reason is that relu goes flat in only one part of the graph. while sigmoid goes flat in two places. for gradient descent this flat in only one part is faster.

Why do NN need activation functions?

Without an activation function, the NN would just be a linear combination of the input and the weights. This would limit the NN to only learning linear relationships. With an activation function, the NN can learn non-linear relationships.

Rectified Linear Unit (ReLU) Activation.
a = max(0, z)

Multiclass Classification.
y can take on more than 2 values but a small number of values.

Softmax Algorithm. Sotmax algorithm is a generalization of the the logistic function to multiple dimensions.
model = Sequential(
    Dense(units=24,activation='relu'),
    Dense(units=4,activation='relu'),
    Dense(units=10,activation='softmax'
)
model.compile(loss=SparseCategoricalCrossentropy())

model.fit(X,Y, epochs=100) 

/// now lets see the reommended version in Tensor Flow
