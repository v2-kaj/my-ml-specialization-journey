Collaborative Filtering

Given ranking of [5,0] by user 1 on movie 1, then w1.x1 + b1 should be approx 5.
If user 2 ranked [0,5] by user 2 on movie 1 then w2.x2 + b2 should be approx 0

Then what features of x1 should there be. Looking at w1.x1 + b1 = 5(let's assume b1 to be 0)
Then x1 should be [1,0]. w1.x1 = 5 and also w2.x2 = 0 which is what is given. 

Note that w1.x1 is the dot product of the two vectors (where you multiply corresponding elements and add the results)

Now, let's come up with a cost fn for learning the values of the features.
In collaborative filtering, wWe are able to guess the values of the features only because we have parameters for many users eg 5 users. If we only have ratings from 1 user then we wouldnt have enough data to guess x.

Given w1,b1, w2,b2, w3,b3, ..., wn,bn 
to learn xi: 
(minimize MSE as usual)
J(xi) = 1/2 sum j:r(i,j)=1(( wj.xi + bj - yij)squared + regularization term) Here if we minimize this then we'd be choosing the features xi for movie i so that for all users j who rated the movie i we try to minimise the squared difference between what they rated and the predicted rating.

Now if we wanted to learn all the features, we can take the cost fn on top and sum it over all the movies.
J(x1, x2, x3, ..., xnm) = 1/2 sum from i = 1 to m ( sum j:r(i,j)=1(( wj.xi + bj - yij)squared + lambda/2 sum from i = 1 to m sum(xik)squared))

This is remarkable because it allows the model to figure out the features while in the models we have seen so far, we've had to provide the features to the model.

Now how do we learn the parameters w and b?

Cost function
J(w, b, x) = 1/2 sum i,j:r(i,j)=1 sum(wj.xi + bj -y(ij)squared )+ lambda/2 sum from j=1 to nu sum k=1 to n (x ki squared)

How do we minimize the cost function? Well we  can use GD. ie.
Repeat Until convergence
    wi = wi - alpha djdw J(w,b,x)
    b = b - alpha djdb J(w,b,x)
    xik = xik - alpha djdxik J(w,b,x)

We now have a collaborative filtering algorithm. The name collaborative filtering is from the sense that because multiple users have given you the ratings, the collaboratively gives you a sense of what  the movie is like allowing us to guess the features of the movie and that in turn allows us to us to predict how other users may rate that movie.

So far our problem formulation... did they user like, interact with an item. Lets now look at the generalization of the collaborative filtering to binary labelling eg whether they use would like, engange with an item.

A common usecase of collaborative filtering is deciding which products to recommend to a user. Given binary labels from user eg 1 if the liked the product otherwise 0 then we can use collaborative filtering to figure out which users would also like the product.


Next Tensorflow Implememtation of CF algorithm.

Lets say we had J = (wx - b)^2

w = tf.Variable(3.0) # initializes w to 3 w is a param that we would like to optimize
x = 1
y = 1
alpha = 0.01
iterations = 30
for iter in range(iterations):
    # user TensorFlow gradient tape to record the steps
    # used to compute the cost J, to enable auto differentiation
    with tf.GradientTape() as tape:
        fwb = wx
        costJ = (fwb - y)**2

    # use gradient tape to calculate the gradients
    # of the cost with respect to the parameter w.
    [dJdw] = tape.gradient( costJ, [w])

    # Run one step of gradient descent by updating 
    # the value of w to reduce the cost.
    w.assign_add(-alpha * dJdw)

This is auto diff aka auto grad but the correct technical term is auto diff.


Now lets take the above and use it to implement Collaborative filtering.

Implementation in Tensorflow

optimizer = keras.optimizers.Adam(learning_rate=1e-1)

iterations = 200
for iter in range(iterations):
    # use TensorFlow's GradientTape 
    # to record the operations used to compute the cost
    with tf.GradientTape() as tape:
        # compute the cost (forward pass is included in the cost)
        cost_value = cofiCostFuncV(X, W, b, Ynorm, R, num_users, num_movies, lambda)

        # use the gradient tape to automatically retrieve
        # the gradients of the trainable variables with respect to the loss
        grads = tape.gradient( cost_value, [X,W,b])

        # run one step of gradient descent by updating the 
        # the value of the variables to minimize the loss
        optimizer.apply_gradients( zip(grads, [X, W, b]))

