Principal Component Analysic

Unsupervised Learning algorithm. Commonly used for visualization if you have data that many features {say 5000 fetaures} that you cant plot. It reduces the features into say 2 features that you can visualize.

Eg take only those variables that vary significantly.

In practice PCA is used to reduce the large number of features eg 50 Dimensional Data into very few eg 2 or 3 features so you can visualize them.

One note on preprocessing. Features should be normalized to have zero mean. also feature scaling.

PCA is not the same algorithm as Linear regression.

Using Scikit learn algorithm.
Fit function includes mean normalization

Less applications for PCA
-Data compression.
-Using it to speeed up the training of NN

Nxt is Reinforcement Learning.
In ML, reinforcement learning is one of the pilars of ML despite being not being widely applied in commercial application.

State x, action y

reward function - if the helicopter is flying well give it a reward of +1 or -1000 if it is not doing so good.

Applications of reinforcement learning.
1. Controlling robots
2. Factory optimization
3. Financial (stock) trading
4. Playing games (including video games)

Reinforcement learning - rather than you explicitely telling the algorith this is the correct oupt y for evry single input. All you have to do instead is specify a reward function that tells it when its doing well or badly and the algoithm to figure out how to chooses the right actions. 


