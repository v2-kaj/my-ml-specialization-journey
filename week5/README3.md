**Decision Trees**

Information Gain creteria lets you decide how to choose one feature to split at one node.

Calculate Information Gain for each of the features, chose the feature with the highest IG.

Split the dataset into the left and right branches using the chosen feature.

Recursively repeat selection of features and spliting until the stopping creteria is reached ie: when a node has all the examples in one class or when spliting a node will exceed maximum depth or another stopping creteria is reached.

One Hot Encoding:
If a categorical feature can take on say k values eg(animal feature which can be dog, cat or mouse) then we can replace that feature with k new binary features ie isDog, isCat or isMouse. For any observation, only one of these k features will have the value 1 while all others will be 0s. This is why it is called "one-hot encoding" only one category is "hot" (active) at a time.

One-hot encoding allows us to convert categorical values say [dog, cat, mouse] into binary vectors containing 0s and 1s that we can feed into a neural network since neural networks work with numerical data. The value 1 represents the presence of a category, while 0 represents its absence. For example, for the categories [Dog, Cat, Mouse], the value [1,0,0] represents that the observation belongs to the Dog category, while Cat and Mouse are absent.

NOW, how about features that can take on continous values ie can assume a specific numerical value within a range of infinitely many possible numbers and not just discrete/categorical values?

Try different potential candidate thresholds eg weight<10, weight<15.5, weight<20.9 etc for each threshold calculate the information gain to determine how good the split at that threshold will be.Choose the feature candidate threshold that has the highest information gain ie maximises reduction in impurity. For n distinct sorted values of a feature, there can be n-1 potential candidate split points to try to split the examples on.

Note that even though a continous feature can theoretically take on infinitely many possible values, decision trees don't have to search infinitely many possible split points. Given a finite training dataset, only a finite number of distinct split points is needed ie any values between any two adjacent training example values. For instance weights of 3.0, 4.0, 5.0 etc, we can use 3.5, and 4.5 as candidate split points. In this case we have decided to use midpoints but any values between any two adjacent values would produce the same partions.