 # Basics

As I introduced very basic what Reinforcement Learning is in the series hub. There are 4 basic terms which are worth to know when reading around RL stuff, a policy, a reward signal, a value function and environment model. I will skip the model as we will explore model-free learning for now. We will get back to it later.

- **Policy** – the core of RL agent. It is the way in which it will behave. It might be a lookup table, function or maybe something complex like Deep Neural Network(?)

- **Reward signal** – the instant gratification. A numerical value which an agent will receive immediately after the action. Maximizing it is an ultimate goal of RL system and it’s used to change the policy. It’s like giving candy to a puppy or saying bad dog 🐕.

- **Value function** – the long-term vision. It’s the function describing possible reward in a long run given the state. It might be the case that the constant small reward will be much better than occasional huge one. Or it might be otherwise.

# Exploration and exploitation

The RL agent is like a puppy. It might figure out that the second bowl contains even better stuff than the first. But while eating it will not see the big steak hiding just behind the corner. The greedy agent will do the same. It will stick to the first pot of reward and exploit it. **It always takes actions which maximize the reward and will never realize there might be even bigger one few steps from it**. That’s why we need **exploration** which is basically the random chance that our system will take random action.

However, there is a problem. We can’t just max out exploration mindlessly as an agent will waste too much time looking for an answer instead of using what it learned. One way of dealing with that is starting with high exploration rate and lowering it the more experienced our system becomes. That is also famous mathematical **exploration vs exploitation** problem. If you can, please solve it 🙏.

# K-armed bandit problem
You all know the famous slot machine aka ‘one-armed bandit’. If you don’t get a pun, it’s simple. It will take your money. Anyway, you have to pull the lever and there is let’s assume random chance of getting some monetary reward. It’s random so we won’t train RL system to pull one lever. But imagine a slot machine with K levers. And each lever gives a random reward but from slightly different range. That way some levers will be different than others. We want to train a simple agent to solve this problem for us. And we want to test greedy algorithm vs exploring one.

# Data
Assuming we are solving k=10 armed bandit problem, I wrote 2 tiny utility functions to generate data. It’s all about normal distribution here to get some random yet predictable data. That way some actions will be generally better than others.

```python
def generate_problem(k):
    return np.random.normal(loc=0.0, scale=1, size=10)

def generate_reward(problem, action):
    return np.random.normal(loc=problem[action], scale=1)
```

# Algorithm
As I mention and will mention again, the idea and the problem comes from the book Reinforcement Learning: An Introduction. I am just learning and writing about it to become better at it.

So there is still something to cover before I jump to the code itself. The value function noted as q*(a) is the real value function. It could be the mean reward for given action. But if the agent would know one, there is no point in training it. The algorithm we will write will estimate the value function and use it to guide its decision. This estimate is noted as Q(A). (Note: I will try to keep it math free or simplified, more in form of a code than equations).

```python
def k_bandit(problem, k, steps, exploration_rate):
    Q = {i: 0 for i in range(k)} # 1. Value function
    N = {i: 0 for i in range(k)} # 2. Number of actions, for update rule
    
    for i in range(steps): # 3. Main loop
        explore = random.uniform(0, 1) < exploration_rate 
        if explore:
            action = random.randint(0, k - 1) # 5. Exploration: Choosing random action
        else:
            action = max(Q, key=Q.get) # 6. Choose action with maximum mean reward
            
        reward = generate_reward(problem, action) # 7. Get reward for current action
        N[action] += 1 # 8. Update action number
        Q[action] += (1 / N[action]) * (reward - Q[action]) # 9. Update value dict
```

So the algorithm is following for each k-learning bandit problem.

1. Create value dictionary. We will use action number as a key and mean reward as a value. Simplest possible way here. Initialize all keys with 0.
2. Create action count dictionary. We need those for the update value dictionary rule. Initialize all keys with 0.
3. for loop with given number of steps or while loop to run infinitely.
4. Exploration. We are checking if algorithm should explore or not. In order to do so, I generated a random number from range 0 to 1 and compared it against exploration rate.
5. If algorithm will explore, we are choosing a random action to perform.
6. In another way, we choose the action defined by the key of Q dictionary with the maximum value assigned.
7. Getting the reward!
8. Increment action count dictionary.
9. The update rule. Book authors noted that this is important and will be used frequently in RL.

So this is it. I was amazed how simple was to create my first Reinforcement Learning agent. I know this is a rocky path but the introduction was pretty gentle.

# Results

I ran the algorithm many times with different exploration rates: 0.0 (greedy bastard!), 0.01, 0.02, 0.1, 0.2. And it gives an interesting perspective on the exploration vs exploitation problem. Let’s look at the charts from the individual runs.

![](https://harderchoices.files.wordpress.com/2018/01/unknown-2.png?w=925)
![](https://harderchoices.files.wordpress.com/2018/01/unknown-3.png?w=925)
![](https://harderchoices.files.wordpress.com/2018/01/unknown-4.png?w=925)

It’s hard to draw a conclusion from the single runs like that. The exploring algorithms seem to perform better but not always the case. If the greedy algorithm got to the optimal answer in the first try it’s hard to beat it. Let’s see how it looks on the bigger picture average on 2000 different problems.

![](https://harderchoices.files.wordpress.com/2018/01/unknown.png?w=925)

Now it’s clear. On the early steps, all algorithms are pretty equal. First, those learning fast are getting an advantage. But then those learning a little with more experience are heading to the top. The greedy one is at the bottom.

# Conclusion

If you followed me during this, congrats! 😃 We wrote 1st RL together. I mean it is a pretty big deal. Although the problem is simple (some might say useless) it explains the exploration vs exploitation dilemma and why it’s important to be aware of it from day 1. Wait for more to come soon! I have some thoughts about using this knowledge in real life software. It might be possible to have such system on a backend learning which element – lever (say button) to use based on user interaction. What do you think? Makes sense?