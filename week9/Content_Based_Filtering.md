Collaborative filtering vs Content-based filtering

In collaborative filtering we recommend items to you based on ratings of other users who provided similar ratings as you on the ratings of items you did rate.

In content-based filtering recommends items to you based on features of items and features of users to find a good match.

r(i,j) = 1 or 0 whether user j has rated item i
y(i,j) the rating the user j has provided on item i

Features of the user and features of the item to find the items to recommend.

In collaborative filtering we predict rating of user j on item i using:
w(j).x(i) + b(j)

In content-based filtering we use;

Vu(j) for Vector of numbers computed for user j (features of the user)
Vm(i) for Vector of numbers computed for movie i (features of the item)

Let's say Vu(j) captures preferences of the user eg [0.6,0.1,9,2,...1.9] say the first number captures how much they like romance movies ie 0.6 and the second is liking of action movie 

and if Vm(i) say [0.7,0.1,7,1.5,...8] say the first number calculating how much this movie is a romance movie.

Then the dot product of the two tell us the predicted rating of the user j on movie i

The challenge is how do we compute Xu(j) and Xm(i)

Implementing Content-Based filtering

A good way to develop CBF algorithm is to use Deep Learning.

Given feature vector describing a user eg age, gender, location etc we have to compute a vector Vu. similary given a vector describing a movie eg genre, stars in the movie, year  we have to compute a vector Vm.

In order to computer Vu, the user network.
the user network takes Xu List of user features eg  alist (age,gender,location) using afew dense layer it will output Vu that describes the user.
The output layer has 32 Units ie Vu is a list of 32 numbers unlike most output layers that have 2 or 3 units.

Similarly to comput Vm we can have a movie network, features of the movie as input layer and the network outputs say 32 units. the output layer of the movie and output layer of the user network have to have the same dimensions hence 32 units and then 32 units. Hypothetically, the user network and the movie network can have different numbers of hidden layers or units in the layers.
 
Prediction will be Vu dot product Vm. This is to predict the rating of the user on the movie. 

If the user liked/favorite an item, to predict whether the user will like/favorite the item, we can modify the algorithm by applying the sigmoid function g(Vu dot product Vm) ie to predict the probability that y(i,j) is 1 (probability that a user will like the item.)

Cost function J = Sum(Vuj.Vmi - yij)squared + NN regularization term

You can also use this model to find similar items just like coraborative filtering algorithm.

Vuj is a vector of length 32 that describes user j with features xuj
and similarly 
Vmi is a vector of lenth 32 that describes movie i with features xmi.

Now what if you wanted to find movies similar to movie i

Well Vmi describes the features of movie i, then we can || Vmk - Vmi|| squared is small. This can be pre-computed eg run a server overnight to compute similar items.

One of the advantages of using a NN is that it is easier to put together several neural networks to work together to build a larger system. And this is an axample of this implementation.

Scaling the model to work on many items or movies.

Todays recommender system often need to pick out a handful of items to recommend to the user. How can we calculate this efficiently for large set of movies?

Many recommender systems are created as two steps.
Retrieval and Ranking steps.
Retrieval - Generates a large list of plausible item candidates.
    For each of the last 10 movies watched by the user find 10 most similar movies

    for most viewed 3 genres find the top 10 movies
    Top 20 movies in the country

Combine retrieved items into list removing duplicates and items already watched/purchased.

Ranking step:
Take a list of retrieved items and rank them using a learned model.
display ranked items to a user.

How many items should we retrieve?
Retrieving more items results in better perfomance but slower recommmendations
To analyze/optimize the trade off, carry out offline experiments to see if retrieving additional items results in more relevant recommendations p(yij) = 1 of items displayed to the user.

Next: TF Implementation of colaborative filtering.


num_outputs = 32

tf.random.set_seed(1)
user_NN = tf.keras.models.Sequential([
    ### START CODE HERE ### 
    tf.keras.layers.Dense(256, activation='relu'),
    tf.keras.layers.Dense(128, activation='relu'),
    tf.keras.layers.Dense(num_outputs)  
    ### END CODE HERE ###  
])

item_NN = tf.keras.models.Sequential([
    ### START CODE HERE ###     
    tf.keras.layers.Dense(256, activation='relu'),
    tf.keras.layers.Dense(128, activation='relu'),
    tf.keras.layers.Dense(num_outputs)
    ### END CODE HERE ###  
])

# create the user input and point to the base network
input_user = tf.keras.layers.Input(shape=(num_user_features))
vu = user_NN(input_user)
vu = tf.linalg.l2_normalize(vu, axis=1)

# create the item input and point to the base network
input_item = tf.keras.layers.Input(shape=(num_item_features))
vm = item_NN(input_item)
vm = tf.linalg.l2_normalize(vm, axis=1)

# compute the dot product of the two vectors vu and vm
output = tf.keras.layers.Dot(axes=1)([vu, vm])

# specify the inputs and output of the model
model = tf.keras.Model([input_user, input_item], output)

model.summary()





