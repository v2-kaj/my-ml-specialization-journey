Decision Trees

IG creteria lets you decide how to choose one feature to split at one node.

Calculate IG for each of the features, chose the feature with the highest IG.

Split the dataset into the left and right branches using the selected feature.

Keep repeating until the stopping creteria is reached ie: when a node is 100% one class or when spliting a node will exceed maximum depth or another creteria.


One Hot Encoding:
If a categorical feature can take on say k values then we can replace that feature with k new binary features. For any observation, only one of these k features will have the value 1 while all others will be 0s. This is why it is called "one-hot encoding" only one category is "hot" (active) at a time.

One-hot encoding allows us to convert categorical values say [dog, cat, bird] into binary vectors containing 0s and 1s that we can feed into a neural network since neural networks work with numerical data. The value 1 represents the presence of a category, while 0 represents its absence. For example, for the category [Dog, Cat, Bird], the value [1,0,0] represents that the observation belongs to the Dog category, while Cat and Bird are absent.

NOW, how about features that can take on continous values ie can assume a specific numerical value within a range of infinitely many possible numbers and not just discrete/categorical values?