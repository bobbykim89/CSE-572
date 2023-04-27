## 1. Which reinforcement learning solution requires the problem to be divided in to subproblems: 
- Dynamic programming
## 2. How can you mitigate the weakness of Greedy Policy for Monte Carlo methods?
- By using ε-greedy policy
## 3. What is the difference between 
$V_\pi$ and $Q_\pi$
- $V_\pi$ is the value function for the policy starting from a given state, whereas $Q_\pi$ is the value function of the policy for performing an action, starting from a given state.
  - Correct! Q value is a restricted Value function that only applies to an action in a given state.
## 4. What is the similarity between Monte Carlo (MC) and Temporal Difference Learning (TDL)?
- Not needing a perfect model of environment. 
## 5. In what case can you use DP for solving RL problems?
- When you have a perfect model of environment
## 6. Select all the methods used in Dynamic Programing in RL.
- Repeat evaluation and improvement until convergence
- Start with an arbitrary policy
- Need to have the perfect model of environment
## 7. For dynamic programming, what do we mean by Policy Improvement?
- Improve π from Vπ
## 8. For dynamic programming, what do we mean by Policy Evaluation?
- Compute Vπ from π
## 9. What are the main differences between Reinforcement Learning (RL) and Markov Decision Process (MDP)? Select all that apply. 
- RL doesn’t assume that you have a model
## 10.  How does Reinforcement Learning overcome not having a complete model of the system?
- By learning from the environment 
- By learning from Sample Episodes of Simulated Experience