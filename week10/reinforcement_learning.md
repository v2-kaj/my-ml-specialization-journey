Nxt is Reinforcement Learning.
In ML, reinforcement learning is one of the pilars of ML despite it not being widely applied in commercial applications.

State x, action y

Reward function - if the helicopter is flying well give it a reward of +1 or -1000 if it is not doing so good.

Applications of reinforcement learning.
1. Controlling robots
2. Factory optimization
3. Financial (stock) trading
4. Playing games (including video games)

Reinforcement learning - rather than you explicitely telling the algorithm this is the correct oupt y for every single input. All you have to do instead is specify a reward function that tells it when it's doing well or badly and the algoithm to figure out how to chooses the right actions. 

The position of an object is called the state. An environment can have several states. 
We control the robot by providing rewards in different states. eg state 6 given a reward of 100 and state 2 may have a reward of 40.

Terminal state - the final state of an object.

At any point the robot is in some state s, choose an action a, and enjoys a reward for being in state s r(s),  end up in a new state s'.

How do you know if a set of reward is better than the other?

Return = 0 + 0 + 0 + 100 the return is weighted factor. 0 + 0.9(0) + 0.9^2x0.9 + 0.9^3*100

Lets call the discount factor gamma r

So to generalize we have R1 + r*R2 + r^2*R3 + r^3*R4. The r has the effect of making the reinforceent abit impatient. since it gives full credit to the first reward. and gives less credit to the second and less and less/..

For most reinforcement learning algorithm, the r is a number closer to one eg 0.9 or 0.5 It's like a time value of money. or the interest rate. The returns depends on the rewards and the rewards depend on the actions.


# The state-action value function definition Q

Q is a function of s and a action you can take in that state.

Returns the return eg Q(s, >) = 0 + (0.5)* 0 + (0.5^2)*0 + (0.5^3)*100 = 12.5
Another example Q(s, <) = 0  + (0.5)*100 = 50
Q(4,<) = 0 + (0.5)*0 + (0.5^2)*0 + (0.5^3)*100 = 12.5

Because the state value action function is denoted with Q. It is also called the Q function or the optimal Q function or the Q*.

The best possible return from state s is the max Q(s,a)
The best possible action in state s is the action a that gives max Q(s,a)

Increasing the discount factor to say closer to 1 eg 0.9 makes the mars rover less impatient. 

Lowering the discount factor makes the alg incredibly impatient.

Bellman equation

Q(s,a) = Return if you
        . start in state s
        . take action a (once)
        . then behave optimally

s: current state
R(s): reward of the current state
a: current action
s': state that you get to after taking action a
a': action that you might take in state s'

The bellman equation

Q(s,a) = R(s) + r*max(Q(s',a))

The goal of reinforcement learning is 
Choose a policy pi(s) = a that will tell us what action a to take in state s so as to maximise the expected return. 

Bellman Equation: Q(s,a) = R(s) + r max Q(s',a')

For a stochastic reinforcement problem:
Bellman Equation: Q(s,a) = R(s) + r E[max Q(s',a')]


NEXT: Continous State spaces: In a contious state reinforcement learning problem / Continous state markov decision process

A robot can be 3.1km along a path. The state might not be 1 number eg its x,y,z, postion, angle of orientation its speed ie it's a vector of continous values.

Learning the state-action value function.

Deep Reinforcement learning

Initialize neural network randomly as guess of Q(s,a)
Repeat {
        Take action in the lunar lander. Get (s,a,R(s),s')
        Store 10000 most recent (s,a,R(s),s') tuples

        Train neural network:
                create a training set of 10000 examples using 
                x = (s,a) and y = R(s) + r max Q(s',a')
                Train Qnew such that Qnew(s,a) = y
        Set Q to Qnew
}

This is the DQN algorithm. Deep Q network algorithm.

To optimise the algorithm, instead of running 4 inferences, lets train the network to output 4 units so that at any input we should only run one inference and get all 4 outputs and pick the action a that maximises Q(s,a)

In the algorithm that we've just used, we need to pick some actions while we are learning. When you're in some state. 

When we are in some state s,
Option 1:
        Pick the action a that maximises Q(s,a)
Option 2:
        With probability 0.95, pick the action that a that maximises Q(s,a) "Greedy" "Exploitation"
        With probablity 0.05, picke and action a randomly "Exploration"
This second option has a name called e-greedy policy e = 0.05

You may start with a high e and then gradually decrease it so that you try to ues the greedy policy


Mini-batch gradient descent. - to avoid scanning over all the training examples in order  to cmpute the derivative on the next step (take a tiny step - and then rrpeat)
The idea of mini-batch is to pick a smaller number of training examples eg m' Then each iteration requires only looking at m' examples.

Soft update 
W = 0.01Wnew + 0.99W
B = 0.1Bnew + 0.99B

So Q = 0.01Qnew + 0.99Q

Soft update causes the algorithm to converge much more reliably.

Limitations of reinforcement learning

1. Much easier to get it working in a simulation than in a real robot.
2. Far fewer applications of reinforcement learning than supervised and unsupervised learning.


Final chapter: Practice lab
