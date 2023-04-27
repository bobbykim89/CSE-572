# Reinforcement Learning
- more general than supervised/unsupervised learning
- learn from interaction w/environment to achieve goal
We have an agent that explores the environment using actions. Each of these explorations have a reward.

## differences
- reinforcement does not assume prior knowledge
- markov chain assumes you already have a model of the environment

## robot in a room
- we want to maximize reward for stochastic robot moving around.
- Robot explores environment and figures shortest path to get +1 state.
- What strategy should robot take to reach max reward?
  - should you go up/down/left/right?
  - 80% chance you go up but 20% chance you don't
  - For each location you have a different strategy.
  - if you get rid of stochastic, then on deterministic the strategy is set.
  - strategy == policy

Goal: explore the environment and learn the strategy, 

## markov decision process
- you have a set of states S, set of actions A, and initial state So
- you have a transition model P(s,a,s')
- you have a reward function r(s)
- **Goal is to maximize cum reward in the long run**
- **policy: mapping from S to a**

## reinforcement learning issues:
- transitions and rewards not available
  - difficult to learn either of these
  - you get them as you explore the environment
- how to change policy based on experience
  - initial policy evolves with exploration
- how to explore the environment
  - how do you change step to get new knowledge

## computing return from rewards
- episodic (vs continuing tasks)
  - limit the execution to N steps
  - optimal policy depends on N
  - game over after N steps
- additive rewards
  - reward can grow and become infinite
- discounted rewards
  - value bounded if reward bounded

## value functions
- state value function $V^\pi(s)$
  - expected return when starting state s and following policy $\pi$
- state-action value function $Q^\pi(s,a)$
  - expected return when starting state s and performing action a AND THEN following policy $\pi$
- useful for finding optimal policy
  - can estimate from experience
  - pick the best action using $Q^\pi(s,a)$
    - so you can evaluate actions in Q values that result from it.
    - Q value is useful for finding optimal policy in a greedy manner
- Bellman equation

$$ V^\pi(s) = \sum_a\pi(s,a)\sum_{s'}[r^a_{ss'}+\gamma V^\pi(s')] = \sum_a \pi(s,a)Q^\pi(s,a) $$

## Optimal value functions
- there is a set of **optimal** policies
  - $V^\pi$ defines partial ordering on policies
  - they share the same optimal value function
$$ V^*(s)=\max_\pi(V^\pi(s))$$

- Beelman optimality equation
  - System of n non-linear equations
  - Solve for V*(s)
  - Easy to extract the optimal policy

$$ V^*(s) = \max_a\sum_{s'}P^a_{ss'}[r^a_{ss'}+\gamma V^*(s')]$$
  
- having $Q^*(s,a)$ makes it even simpler: 

$$ \pi^*(s) = arg \max_a Q^*(s,a) $$