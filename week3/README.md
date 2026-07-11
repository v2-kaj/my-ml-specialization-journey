Neural Networks aka Artificial NN

In week 3 I Learn about Neural Networks also called Deep Learning Algorithms and the Decision Trees

Application first in speech Recogn, computer vision, text (NLP)

With increasing amount of data linear and logistic performances didnt improve much. 

Now lets look at NN using demand prediction example.

Layer - a grouping of neurons which take as input the same or similar inputs. Can have one or more neurons
The output layer - outputs the final predictions of the neural network

Activattion - a degree that neuron sends high output values or many values to other neurons

Input layer is a list of inputs into a neural network.

In a neural network each layer is a vector and inputs into another layer which in turn outputs a vector which is then an input into another layer and so on and so fourth.

Each neuron receives features encoded as a vector or numbers. The neuron then assigns weight to each feature. The neuron then calculates the weighte sum of the features by multiplying each feature by its weight. It then adds a bias to the sum. This sum is now becomes the neuron's input. The neuron then applies an activation function on this neuron's input to determine if the neuron should be activated or not. The main role of the activation function is to introduce non-linearity into the model allowing the network to learn more complex patterns.

The middle layer are called hidden layers as they are not obvious as input and output layers.

The output of each layer is passed through an activation function to determine if the neuron should be activated or not.

NN is sort of logistic regression but that can learn the most important features on its own to ouput a more likely output. In logistic regression, we do manual feature engineering but NN do this on their own.

How many hidden layers, and how many neorons in the hidden layer this is the architecture of the neural network. This does have impact on the performance of the NN.

Multi layer perceptron is a type of neural network that has multiple layers of neurons.

Activations are higher level features.

Forward propagation Algorithm.

Units means neurons
