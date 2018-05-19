# What is dynamic programming?

Behind this strange and mysterious name hides pretty straightforward concept. Dynamic programming or DP, in short, is a collection of methods used calculate the optimal policies – solve the Bellman equations. Before you get any more hyped up there are severe limitations to it which makes DP use very limited. Here are main ones:

- It needs perfect environment model in form of the Markov Decision Process – that’s a hard one to comply. It’s fine for the simpler problems but try to model game of chess with a description of all states. Have fun 😉
- Computationally expensive – as I mentioned before solving Bellman equations is a brute force job. Try to do it for a chess game. You will need few orders of magnitudes more computing power then all humanity already has.

So why even bothering checking out the dynamic programming? 🤔 Well, it’s an important step to understand methods which comes later in a book. And the dynamic programming provides us with the optimal solutions. Other Reinforcement Learning methods try to do pretty much the same. Only with fewer resources and the imperfect environment model.

# Testbed

Before we jump into the theory and code let’s see what “game” we will try to beat this time. Here is the board:

```
-----------------
| X |   |   |   |
-----------------
|   |   |   |   |
-----------------
| A |   |   |   |
-----------------
|   |   |   | X |
-----------------
```

The game I coded to be exactly the same as the one in the book. The code to print the board and all other accompanying functions you can find in the notebook I prepared.

- X is the terminal state, where our game ends. It’s the place we want to be as fast as possible.
- A is the agent position.

The agent starts in a random state which is not a terminal state. Every step it needs to take has a reward of -1 to optimize the number of moves needed to reach the finish line. The agent can move in any direction (north, south, east, west). If the move would take the agent out of the board it stays on the same field (s' == s).

Let’s try it out! 🏁

# Random policy

To debug the board, agent code and to benchmark it, later on, I tested agent out with random policy. Which means that on every move it has a 25% of going in any direction. An agent with such policy it’s pretty much clueless. Here is the code for it:

```python
def agent(policy, starting_position=None):
    l = list(range(16))
    state_to_state_prime = create_state_to_state_prime_verbose_map()
    agent_position = randint(1, 14) if starting_position is None else starting_position
        
    step_number = 1
    
    while not (agent_position == 0 or agent_position == 15):
        current_policy = policy[agent_position]
        next_move = random()
        lower_bound = 0
        for action, chance in current_policy.items():
            if chance == 0:
                continue
            if lower_bound <= next_move < lower_bound + chance:
                agent_position = state_to_state_prime[agent_position][action]
                break 
            lower_bound = lower_bound + chance
                
        step_number += 1   
    
    return step_number
```

- policy is a dictionary containing the states as the keys and move chances as a value in form of another dictionary. N, S, E, W moves directions and the float number is a chance of performing it by the agent.
- state_to_state_prime_map is a map similar to the policy but as a value, we have a dictionary with move directions and resulting states (s') after performing that moves.

The dictionaries look like that:

```
// Random Policy
{0: {'E': 0.0, 'N': 0.0, 'S': 0.0, 'W': 0.0},
 1: {'E': 0.25, 'N': 0.25, 'S': 0.25, 'W': 0.25},
 2: {'E': 0.25, 'N': 0.25, 'S': 0.25, 'W': 0.25},
...
 13: {'E': 0.25, 'N': 0.25, 'S': 0.25, 'W': 0.25},
 14: {'E': 0.25, 'N': 0.25, 'S': 0.25, 'W': 0.25},
 15: {'E': 0.0, 'N': 0.0, 'S': 0.0, 'W': 0.0}}

// State to State prime
{0: {'E': 0, 'N': 0, 'S': 0, 'W': 0},
 1: {'E': 2, 'N': 1, 'S': 5, 'W': 0},
 2: {'E': 3, 'N': 2, 'S': 6, 'W': 1},
...
 13: {'E': 14, 'N': 9, 'S': 13, 'W': 12},
 14: {'E': 15, 'N': 10, 'S': 14, 'W': 13},
15: {'E': 0, 'N': 0, 'S': 0, 'W': 0}}
```

What the agent function does is until the terminal state is reached (0 or 15) it creates random float between 0 and 1. Then compares it against current state policy to decide on move and checks which is being’` for that action.

Let’s see how an agent performs with the random policy:

![](https://harderchoices.files.wordpress.com/2018/02/lut-24-2018-15-02-13.gif?w=925)

![](https://harderchoices.files.wordpress.com/2018/02/lut-24-2018-15-02-26.gif?w=925)

![](https://harderchoices.files.wordpress.com/2018/02/lut-24-2018-15-02-22.gif?w=925)

![](https://harderchoices.files.wordpress.com/2018/02/lut-24-2018-15-02-18.gif?w=925)

An average number of steps an agent with random policy needs to take to complete the task in 19.843. Pretty bad, right?

# Back to the Finite Markov Decision Process

We need to get back for a while to the finite-MDP. From this moment it will be always with us when solving the Reinforcement Learning problems. Finite-MDP means we can describe it with a probabilities p(s', r | s, a). Quick reminder:

    p – probability
    s' – resulting state
    r – reward
    s – current state
    a – action

In plain English p(s', r | s, a) means: probability of being in resulting state with the reward given current state and action. The set is exhaustive that means it contains all possibilities even those not allowed by our game. For our simple problem, it contains 1024 values and our reward is always -1! Tell me about the brute force algorithms. 😎 I decided to include this section as this term will appear often in Reinforcement Learning.

# Iterative policy evaluation

This is the first method I am going to describe. Both of theme will use the iterative approach. We will solve Bellman equations by iterating over and over.

```python
def iterative_policy_evaluation(policy, theta=0.01, discount_rate=0.5):
    V_s = {i: 0 for i in range(16)} # 1.
    probablitiy_map = create_probability_map() # 2.

    delta = 100 # 3.
    while not delta < theta: # 4.
        delta = 0 # 5.
        for state in range(16): # 6.
            v = V_s[state] # 7.
            
            total = 0 # 8.
            for action in ["N", "E", "S", "W"]:
                action_total = 0
                for state_prime in range(16):
                    action_total += probablitiy_map[(state_prime, -1, state, action)] * (-1 + discount_rate * V_s[state_prime])
                total += policy[state][action] * action_total   
                
            V_s[state] = round(total, 1) # 9.
            delta = max(delta, abs(v - V_s[state])) # 10.
    return V_s # 11.
```

Two hyperparameters here are theta and discount_rate. Theta is a parameter controlling a degree of approximation (smaller is more precise). Discount rate I described [last time](before and it diminishes a reward received in future.

Let me go with you step by step here.

1. Initialization of V_s dictionary. It contains the value of each state and we will use it to create better policy which will choose next state based on maximum value. Remember to set terminal states values to 0, rest is up to you.
2. Creation of probability map described in the previous section. You can use a global variable or anything. It doesn’t change so you don’t have to create fresh each time.
3. Initialization of delta parameter to some high value (higher than theta).
4. delta goes to 0 for later use.
5. while loop. We will repeat everything until the delta will be smaller than theta.
6. for loop iterating through all states.
7. Value assignment of the current state to local variable v for later.
8. Start of summation. The heart of the algorithm is here. There are 2 sums here hence 2 additional for loops. action_total is a sum of probabilities for each action while total is a sum of all action sums. You can find math in a Reinforcement Learning: An Introduction (Book site | Amazon).
9. Assignment of total which is a new estimated value for current state to V_s dictionary containing all values.
10. New delta which can stop the while loop.
11.. Return of V_s dictionary to create new policy later on.

```
policy = create_random_policy()
V_s = iterative_policy_evaluation(policy) # {0: 0.0, 1: -1.7, 2: -1.9, 3: -1.9, 4: -1.7, 5: -1.9, 6: -1.9, 7: -1.9, 8: -1.9, 9: -1.9, 10: -1.9, 11: -1.7, 12: -1.9, 13: -1.9, 14: -1.7, 15: 0.0}
policy = create_greedy_policy(V_s)

V_s = iterative_policy_evaluation(policy) # {0: 0.0, 1: -1.0, 2: -1.5, 3: -1.8, 4: -1.0, 5: -1.5, 6: -1.8, 7: -1.5, 8: -1.5, 9: -1.8, 10: -1.5, 11: -1.0, 12: -1.8, 13: -1.5, 14: -1.0, 15: 0.0}
policy = create_greedy_policy(V_s)
```

The algorithm managed to create optimal solution after 2 iterations. More is just a value tuning. It averages around 3 steps per solution. That’s quite an improvement from the random policy!

![](https://harderchoices.files.wordpress.com/2018/02/lut-24-2018-15-05-59.gif?w=925)

![](https://harderchoices.files.wordpress.com/2018/02/lut-24-2018-15-06-06.gif?w=925)

![](https://harderchoices.files.wordpress.com/2018/02/lut-24-2018-15-06-03.gif?w=925)

![](https://harderchoices.files.wordpress.com/2018/02/lut-24-2018-15-06-09.gif?w=925)

# Value iteration

Value iteration is quite similar to the policy evaluation one. But the approach is different. First of all, we don’t judge the policy instead we create perfect values. Let’s tackle the code:

```python
def value_iteration(V_s, theta=0.01, discount_rate=0.5):
    value_for_state_map = create_value_for_state_map() # 1.

    delta = 100 # 2.
    while not delta < theta: # 3.
        delta = 0 # 4.
        for state in range(1, 15): # 5.
            v = V_s[state] # 6. 
            
            totals = {} # 7.
            for action in ["N", "S", "E", "W"]:
                total = 0
                for state_prime in range(16):
                    total += value_for_state_map[(state_prime, -1, state, action)] * (-1 + discount_rate * V_s[state_prime])
                totals[action] = total
            
            V_s[state] = round(max(totals.values()), 4) # 8.
            delta = max(delta, abs(v - V_s[state])) # 9.
    return V_s # 10.
```

Points #1 - #6 and #9 - #10 are the same as #2 - #7 and #10 - #11 in previous section. The only difference is that we don’t have to create the V_s from scratch as it’s passed as a parameter to the function. The for loop iterates through all states except the terminal states. The reason is that we don’t want to mess with terminal states having a value of 0. We don’t have any other way (like a positive reward) to make this states distinguished.

1. Start of summation. Here we calculate values for each action without summing it together like in the previous point. We have to store all values.
2. Assignment of value for state. Here the value of the state is a value of maximum action.

I won’s show you the test runs of the algorithm as it’s the same as the policy evaluation one. Dynamic Programming methods are guaranteed to find an optimal solution if we managed to have the power and the model.

# Conclusion

The Dynamic Programming is a cool area with an even cooler name. It shows how Reinforcement Learning would look if we had superpowers like unlimited computing power and full understanding of each problem as Markov Decision Process. I found it a nice way to boost my understanding of various parts of MDP as the last post was mainly theoretical one. I hope you enjoyed. Coming up next is a Monte Carlo method. 👋