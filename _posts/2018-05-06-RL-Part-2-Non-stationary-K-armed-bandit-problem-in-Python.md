Recently I described simple K-bandit problem and solution. I also did a little introduction to Reinforcement Learning problem. Today I am still going to focus on the same problem with a little bit more terminology and few different algorithms (or more like few different variants). I am not going to exhaust the topic as it’s pretty broad and well studied but to give myself and you dear reader some overview on it. Let’s begin.

# Stationary vs Non-stationary

In the last post, I presented one simple algorithm in 2 variants. Greedy and Ɛ-greedy ones to solve our K-armed bandit problem. It was an easy mode which was good as an introduction to the subject and not so good as a real-life-like problem. The data which our algorithm operated on was stationary. In plain words:

    Stationary problem – there is always the best answer and it never changes

It doesn’t work that way in a real world! 🌏 Like a data of users, behavior might be different at night or when some event happens. Or the next game level might have some additional obstacle. We would like our algorithms to fins such subtleties.

    Non-stationary – there is always the best answer but it could change any time

# Testbed 🛌

I had to adjust a little bit my problem and reward generation functions to accommodate the non-stationary problem. And as I plot a lot this time I needed to make plotting and comparing stuff easier.

```python
class KBanditProblem:
    
    def __init__(self, k, stationary=True):
        self.k = k
        self.stationary = stationary
        self.values = np.random.normal(loc=0.0, scale=1, size=k)
        self.optimal = self.values.argmax()
        
    def generate_reward(self, action):
        if not self.stationary:
            self.values += np.random.normal(loc=0.0, scale=0.01, size=self.k)
            self.optimal = self.values.argmax()
        return np.random.normal(loc=self.values[action], scale=1)]
```

What I did was wrapping everything in class to easily pass problem object to a solution object and use it. Really only new thing is a stationary flag. If it’s false then I add to the values normally distributed random numbers with small variance. optimal property is there to count performance of the solution. Yeah, it might be an overkill but I am a software engineer by trade and I just like writing code and optimizing it. I also created a base class for solutions to count the data I needed for plotting charts.

```python
class KBanditSolution:
    
    def __init__(self, problem, steps):
        self.problem = problem
        self.steps = steps
        
        self.average_reward = 0
        self.average_rewards = np.array([])
        self.optimal_percentage = 0
        self.optimal_precentages = np.array([])
        
    def count_statistics(self, action, reward, step):
        self.average_reward += (1 / (step + 1)) * (reward - self.average_reward)
        self.optimal_percentage += (1 / (step + 1)) * ((1 if action == self.problem.optimal else 0) - self.optimal_percentage)
        self.average_rewards = np.append(self.average_rewards, self.average_reward)
        self.optimal_precentages = np.append(self.optimal_precentages, self.optimal_percentage)
```

I wrote two helper functions. One to generate average data over X runs and the other to create charts. My jupyter-notebook is a mess right now but I will publish it when I finish having fun with K-armed bandit.

# Ɛ-greedy solution to a new problem

Long story short. I had to modify a previous solution to accommodate class-based approach. The really new thing is initial_value needed later, for now, it will be always set to 0.

```python
class EGreedy(KBanditSolution):
    
    def solve(self, exploration_rate, initial_value):
        Q = {i: initial_value for i in range(k)} # 1. Value function
        N = {i: 0 for i in range(k)} # 2. Number of actions, for update rule

        for i in range(self.steps): # 3. Main loop
            explore = random.uniform(0, 1) < exploration_rate  # 4. Exploration
            if explore:
                action = random.randint(0, k - 1) # 5. Exploration: Choosing random action
            else:
                action = max(Q, key=Q.get) # 6. Choose action with maximum mean reward

            reward = self.problem.generate_reward(action) # 7. Get reward for current action
            N[action] += 1 # 8. Update action number
            Q[action] += (1 / N[action]) * (reward - Q[action]) # 9. Update value dict 
            self.count_statistics(action, reward, i)
```

And here is its performance on our new problem:

![](https://harderchoices.files.wordpress.com/2018/01/e-greedy-1.png?w=925)

In this kind of problem the more our solution tries to explore the better it performs. On a stationary problem chart, the lines were much closer together.

# Weighted average

As the data in our environment change, it’s short-sighted to assume every data-point has exactly the same value. And that’s what we did up until now. Only point #9 had changed.

```python
class WeightedAverage(KBanditSolution):
    
    def solve(self, exploration_rate, step_size, initial_value):
        Q = {i: initial_value for i in range(k)} # 1. Value function
        N = {i: 0 for i in range(k)} # 2. Number of actions, for update rule

        for i in range(self.steps): # 3. Main loop
            explore = random.uniform(0, 1) < exploration_rate  # 4. Exploration
            if explore:
                action = random.randint(0, k - 1) # 5. Exploration: Choosing random action
            else:
                action = max(Q, key=Q.get) # 6. Choose action with maximum mean reward

            reward = self.problem.generate_reward(action) # 7. Get reward for current action
            N[action] += 1 # 8. Update action number
            Q[action] += step_size * (reward - Q[action]) # 9. Update value dict 
            self.count_statistics(action, reward, i)
```

In Ɛ-greedy we calculated mean to estimate value function (Q) here we use a weighted average. I parametrized only the step_size, the exploration_rate is at 0.1. In Reinforcement Learning: An Introduction all maths are nicely described. The update rule in point #9 is now calculating the weighted average having only previous weighted average value and new value so we don’t have to store all values. Check previous post for why. If you don’t believe the math here go to comments or to the book.

![](https://harderchoices.files.wordpress.com/2018/01/weighted-1.png?w=925)

My goal wasn’t to find the optimal solution but to reproduce algorithms with some personal flair. We can see the results are pretty much on par with the first one. So our new code doesn’t seem to perform much better the last. It’s not useless either, results are quite on par and the chart behaves differently.

# Optimistic vs Realistic

Up until this point, all our algorithms were realistic. That’s what the initial_value parameter is for. The realistic algorithm assumes that the all possible choices at the beginning are not either good (positive value) or bad (negative value). They are just zero and it will figure out on the fly the estimations.

The optimistic solution assumes that all actions could be splendid. That means significantly higher than the real possible values. That gives algorithm an incentive to try it all. Let’s see how it compares.

![](https://harderchoices.files.wordpress.com/2018/01/ovr1.png?w=925)
![](https://harderchoices.files.wordpress.com/2018/01/ovr2.png?w=925)
![](https://harderchoices.files.wordpress.com/2018/01/ovr3.png?w=925)

My conclusion is following. The realistic algorithm starts stronger as it sticks to action more when it finds a good one. But the optimistic catches up. In a long run, optimistic algorithms are (almost) always winning. Life lesson: it’s good to be optimist.
# Upper-Confidence-Bound (UCB) action selection

But can we do better? Sure! By changing not value function estimation calculation but only the action selection method. What this method does is calculate which action to take not by how recent action was. This is the way we did it before. UCB judges an action by its potential. Let’s calculate it first.

![](https://harderchoices.files.wordpress.com/2018/01/ql_2a79054bb8f7513dba71e6fc4b188e68_l3.png?w=925)

Sorry if my math to plain words formula is unclear. We figure out values for each action by adding some things to our actual estimate of action value – Q. Those things are:

- c – exploration parameter, it’s just a hyperparameter, which means we have to optimize it ourselves. c should be bigger than 0
- all actions taken – a count of all actions. Or in other words a current step number
- action count – how many times we took this specific action.

When you take some action your action count grows. all actions taken grows too, but since it’s in a natural logarithm the numerator doesn’t increase as fast. When denominator grows the whole term (which is called uncertainty term) is smaller. Plain 🇬🇧: The more we explore given action, the more certain we are about it and the less certain we are about other actions. It changes for all actions so it makes sure that all actions will be explored. Given enough of steps of course. Here is an actual code:

```python
class UCB(KBanditSolution):
    
    def count_ucb(self, q, c, step, n):
        if n == 0:
            return sys.maxsize
        return (q + (c * sqrt((log(step) / n))))
    
    def solve(self, c):
        Q = {i: 0 for i in range(k)} # 1. Value function        
        N = {i: 0 for i in range(k)} # 2. Number of actions, for update rule

        for i in range(self.steps): # 3. Main loop
            Q_ucb = {i: self.count_ucb(Q[i], c, i + 1, N[i]) for i in range(k)} # 4. Count UCB
            action = max(Q_ucb, key=Q_ucb.get) # 5. Choose action with maximum UCB

            reward = self.problem.generate_reward(action) # 6. Get reward for current action
            N[action] += 1 # 7. Update action number
            Q[action] += (1 / N[action]) * (reward - Q[action]) # 8. Update value dict 
            self.count_statistics(action, reward, i)
```

In point #4 we count UCB dictionary which will our decision be based on. count_ucb function calculates UCB for one action. Dictionary comprehension in #4 makes estimates for whole Q dictionary. Then we take an option with maximum value. Note: It’s important to use big value (like sys.maxsize in my case) when the action had never been taken for everything to work correctly. Again more math in the Reinforcement Learning: An Introduction. Let’s see the results.

![](https://harderchoices.files.wordpress.com/2018/01/ucb.png?w=925)

Nice! If you remember the values for other solutions you can see it’s way bigger. So it looks like we nailed it. But keep in mind that UCB works only well for K-armed bandit problems. It doesn’t generalize to other reinforcement learning problems. 😞

# Summary

Now it’s the time to look at how every solution compares. Here is my totally non-scientific competition with all algorithms described today.

![](https://harderchoices.files.wordpress.com/2018/01/summary.png?w=925)

UCB is a clear winner with both optimistic approaches on a 2nd and 3rd. The realistic one trails on 1000 of steps.

What I hoped to achieve with is post is improve my understanding of Reinforcement Learning further by learning basics. I hope you will find it useful. I had my share of fun. 😄