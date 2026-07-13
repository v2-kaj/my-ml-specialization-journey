Neural Networks aka Artificial NN

In week 3 I Learn about Neural Networks also called Deep Learning Algorithms and the Decision Trees

Application first in speech Recogn, computer vision, text (NLP)

With increasing amount of data linear and logistic performances didnt improve much. 



Now lets look at NN using demand prediction example.

Layer - a grouping of neurons (units) that take as input a set of features represented as a vector. Can have one or more neurons
The output layer - outputs the final prediction of the neural network

Activattion - a degree that neuron sends high output values or many values to other neurons

Input layer is a list of inputs into a neural network also referred to as layer 0 or the network.

In a neural network, each layer is a vector and inputs into another layer which in turn outputs a vector which is then an input into another layer and so on and so fourth up to the output layer which outputs the final prediction.

Each neuron receives features encoded as a vector of numbers. The neuron then assigns weights to each feature. The neuron then calculates the weighted sum of the features by multiplying each feature by its weight. It then adds a bias term to the sum. This sum now becomes the neuron's input. The neuron then applies an activation function on this neuron's input to determine if the neuron should be activated or not. The main role of the activation function is to introduce non-linearity into the model allowing the network to learn more complex patterns in the data beyond simple linear combinations.

The middle layers are called hidden layers as they are not obvious as input and output layers in the sense that you don't inspect their outputs directly unlike the input and output layers.

The output of each layer is passed through an activation function to determine if the neuron should be activated or not.

Neural Network can learn the most important features on its own to ouput a more likely output. In logistic regression or linear regression, we do manual feature engineering but NN do this on their own.

The number of hidden layers, and the number of neurons (units) in each layer defines the architecture of the neural network. This does have impact on the performance of the NN.

Multi layer perceptron is a type of neural network that has multiple layers of neurons.

Activations are higher level features.


Forward prop in python.

def dense(a_in, W, b):
    """
    Args:
      a_in (ndarray (n,)) : Data, 1 example 
      W    (ndarray (n,j)) : Weight matrix 
      b    (ndarray (j,))  : bias vector 
    Returns
      a_out (ndarray (j,)) : vector.
    """

    units = W.shape[1] # number of units in the layer
    a_out =  np.zeros(units)

    for j in range(units):
        w = W[:, j]
        z = np.dot(w, a_in) + b[j]
        a_out[j] = g(z) # g is defined outside this function
        
    return a_out

def g(z):
    # g is our sigmoid function
    return (1/(1 + np.exp(-z)))

Then sequential is 
a1 = Dense(X, W1, b1)
a2 = Dense(a1, W2, b2) #a1 is the activations of first layer
a3 = Dense(a2, W3, b3) #a2 is the activation of the second layer
fx = a3 #final output

def my_model(X, W1, b1, W2, b2, W3, b3):
    a1 = Dense(X, W1, b1)
    a2 = Dense(a1, W2, b2)
    a3 = Dense(a2, W3, b3)
    return a3

def my_predict(X, W1, b1, W2, b2, W3, b3):
    m = X.shape[0]
    p = np.zeros(m)
    for i in range(m):
        p[i] = my_model(X[i], W1, b1, W2, b2, W3, b3)
    return p

Note that weights and biases are learned during training and passed here for forward propagation to output the node values.

As an example we can now say:

yhat = (my_predict(X, W1, b1, W2, b2, W3, b3)>0.5).astype(int) to output [0, 0, 1, 0, 1]
for example as out put predictions for each sample in the dataset X.
