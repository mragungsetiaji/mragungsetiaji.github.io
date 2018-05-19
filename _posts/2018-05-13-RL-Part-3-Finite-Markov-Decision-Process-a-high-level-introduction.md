I wanted to avoid making this post as there will be zero code. But as I assumed my series will be stand-alone I have to write it. So to move further I have to first establish a definition of Finite Markov Decision Process. It is a crucial assumption. Solving the problem of Finite Markov Decision Process (or finite MDP) is our main goal in most reinforcement learning.

# What? Who? When? 🤔

Very (very) high-level definition of MDP for me is:

    Markov Decision Process is a framework allowing us to describe a problem of learning from our actions to achieve a goal.

The formal definition (not this one 👆) was established in 1960. This framework is used in many areas like robotics, automation control, economics, and manufacture. Oh, and of course reinforcement learning.

The main components of such process are:

- agent learns, makes decisions and interacts with environment
- environment everything besides the agent

This pair interacts all the time. The agent makes a decision (performs an action) and the environment responds with new conditions and gives rewards. Again as with K-armed bandit problem the agent’s goal is to maximize reward. The interaction occurs at the sequence of discrete time steps. The discrete means that they are well defined, measurable and we cannot split them further. If every second something happens for our agent to respond to it is discrete time. It doesn’t have to be an exact time as minutes or seconds. Our system, for example, could react to some irregular event like a change of conditions or decision request. What’s important there are no steps in between our time steps.

So it goes like this. Agent decides, and it finds itself in a next time steps. It receives a reward and the state changes. In response to the state change agents makes another decision, and so on… The word reward and its value could be confusing at first. In our human language, the sentiment of the word reward is positive. But in reinforcement learning reward could be positive, negative or zero.

![](https://harderchoices.files.wordpress.com/2018/02/mdp.png?w=925)

Markov Decision Process graph

So we defined the MDP. What about finite MDP? That’s an easy one.

    In finite Markov Decision Process the sets of states, actions and rewards are finite

That makes it easier on us when modeling the process and definitely it makes easier for computers to calculate everything.
# Agent – environment boundary

The process is defined by the creators. There is no magic switch or a black box to connect to. We have to engineer everything ourselves. What are rewards? When are rewards given? What are possible actions for that states? What states are possible after that action? There is many more of those and each is crucial to our success. Very important in answering some of the doubts is setting up the agent – environment boundary.

Let’s imagine we would like to build the reinforcement learning system to control the robot. What’s our agent? The easy answer is well the robot is. But is it? Let’s consider a humanoid robot to make an analogy similar to our bodies. The agent has to take actions.

But what are actions? Are they steps or arm movements? If so our agent will need to call high-level functions allowing it to walk or grab something. If not maybe actions are setting up angles of joints in a robot? Like, set the elbow to 15 degrees and the wrist 30 degrees? That’s also a possibility. It could even be the voltage on the motors controlling the movement.

Same story with the states. This boundary is usually not like our body versus the rest. The good framework for thinking about it is following. If the agent is brain the environment is everything else including our body. It’s up to us if we expose a high level function to move an arm or if we would control the tightness of particular muscles. But the muscles are outside. We do not have an absolute control. Something might fail. We are limited by the joints. We might not be able to do something. Our action of moving an arm could render it broken. That’s our environment. We don’t control it absolutely. We control our thinking. We could want to pick up something heavy. But whether we can pick it up or not it’s not only up to us. It’s the weight, strength of our muscles, fatigue level. Things we don’t control directly.

Also, the rewards are external. Rewards are given by the environment not created inside the agent. Let’s go with the picking up analogy again. There could be a negative reward for breaking, dropping the item or even staying idle. The positive reward would be given for completing a goal so if the item is placed in a certain area. But as an agent live to maximize cumulative reward received you can be sure it would maximize the hell a lot of it when controlling its pleasure button. 🔘

# Example

Let’s go further with simple picking up an example. We might define 2 states either there is something to pick up or not. If there is nothing we can not pick up so we can only wait. Otherwise, we can pick up it but also we can wait some more. Each time we wait or pick up an item there is a chance there would be something to pick up or not in a later step. Here is a simple diagram of such situation.

![](https://harderchoices.files.wordpress.com/2018/02/untitled-diagram.png?w=925)

Simple diagram describing the process

Now we have to define probabilities in what state we will end up after taking some action. Each of those (black circles on our diagram) actions will affect the environment somehow. Sum probabilities of states after any action (arrows coming out of the black circle) must equal 1 for Markov Decision Process to be defined correctly. On a diagram below I assumed that there is a flat chance of 80% that there is an item to pick up coming up next. So for any action item will appear with probability 0.8 and will not appear with 0.2 probability.

![](https://harderchoices.files.wordpress.com/2018/02/untitled-diagram-2.png?w=925)

Diagram with probabilities

The last thing is to define rewards. The agent receives the reward for picking the item up. Otherwise, there is to gratification.

![](https://harderchoices.files.wordpress.com/2018/02/untitled-diagram-4.png?w=925)

Diagram with rewards

I know my example is over (over) simplified. The process defined in such way is our Finite Markov Decision Process. Now we are ready to unleash some reinforcement learning techniques on it. We can also describe it in a table in following way.

|state (s) 	|action (a) 	|resulting state (s’) 	|probability of s’ 	|reward|
|---|---|---|---|---|
|nothing 	|wait 	        |something 	            |0.8 	            |0|
|nothing 	|wait 	        |something 	            |1 – 0.8 	        |0|
|something 	|wait 	        |something 	            |0.8 	            |0|
|something 	|wait 	        |nothing 	            |1 – 0.8 	        |0|
|something 	|pick up 	    |something 	            |0.8 	            |R|
|something 	|pick up 	    |nothing 	            |1 – 0.8 	        |R|

Of course, you don’t have to create your process as a graph or table as it might be too complicated. But that’s one way of thinking about it and visualizing. I hope you find it useful.

# Solving

This part should be math. But I would like to skip it. You can always find all the proofs you might need and more in Reinforcement Learning: An Introduction. For a start let’s remind once again a goal of the reinforcement learning system:

    The goal of reinforcement learning system is to maximize total reward.

To be able to estimate future value and policy function later on our agent has to be able to approximate future expected rewards. The expected reward function is just a sum of a current reward and possible future rewards. But should we treat all rewards the same? Should big but uncertain reward in a distant future be better than low but immediate reward? That’s why we need discount rate hyperparameter. It’s the number between 0 and 1. If the discount rate is 0 then future reward doesn’t matter. The 1 value means all future values are equally important. Other values fall in between.

Policy function is a map connecting states to probabilities of selecting a possible action. It defines our agent behavior. Policy function is being learned by an agent to achieve a goal.

Value function is dependent on the state and the policy. It is expected reward value in defined conditions. Again the better we are able to estimate it the agent has better view of the situation.

Traditionally you can solve this problem with Bellman equations. You can really solve it not just estimate for simple problems. The issue is it’s not very useful in practice. It’s pretty much very brute-force computation of all probabilities, states, and values. It’s also based on 3 assumptions which are seldom true:

1. We know pretty much everything about the environment
2. We have computing power
3. Markov property – future depends only on present, not the past

It would be impossible to brute force is for games like chess or go. That’s why reinforcement learning is focused not on solving it but estimating.

# Outro

So that’s enough for the Finite Markov Decision Process. I hope you will find my lengthy definition useful. It’s a gateway from more interesting thins we will explore later on like dynamic programming for a start. If you feel I skipped something or oversimplified please let me know. I wanted to create a high-level overview for myself to better understand the framework.