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

The position of an object is called the state. An env can have several states. 
We control the robot by providing rewards in different states. eg state 6 given a reward on 100 and state 2 may be a state of 40.

Terminal state - the final state of an object.

At any point the robot is in some state s, choose an action a, and gets enjoys r(s), s')

How do you know if a set of reward is better than the other?

Return = 0 + 0 + 0 + 100 the return is weighted factor. 0 + 0.9(0) + 0.9^2x0.9 + 0.9^3*100

Lets call the discount factor gamma r

So to generalize we have R1 + r*R2 + r^2*R3 + r^3*R4. The r has the effect of making the reinforceent abit impatient. since it gives full credit to the first reward. and gives less credit to the second and less and less/..

For most rla, the r is a number closer to one eg 0.9 or 0.5 Its like a time value of money. or the interest rate. The returns depends on the rewards and the rewards depend on the actions.


