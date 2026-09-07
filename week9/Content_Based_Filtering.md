Collaborative filtering vs Content-based filtering

In collaborative filtering we recommend items to you based on ratings of other users who provided similar ratings as you on the ratings of items you did rate.

In content-based filtering recommends items to you based on features of items and features of users to find a good match.

r(i,j) = 1 or 0 whether user j has rated item i
y(i,j) the rating the user j has provided on item i

Features of the user and features of the item to find the items to recommend.

In collaborative filtering we predict rating of user j on item i using:
w(j).x(i) + b(j)

In content based filtering we use;

Vu(j) for Vector of numbers computed for user j
Vm(i) for Vector of numbers computed for movie i

Let's say Vu(j) captures preferences of the user eg [0.6,0.1,9,2,...1.9] say the first number captures how much they like romance movies ie 0.6 and the scond is liking of action movie 

and if Vm(i) say [0.7,0.1,7,1.5,...8] say the first number calculating how much this movie is a romance movie.

Then the dot product of the two tell us the predicted rating of the user j on movie i

The challenge is how do we compute Xu(j) an Xm(i)
